---
sidebar_position: 9
---

## Common Concurrency Patterns in Go


### 1️. Fan-Out / Fan-In

Used to distribute work across multiple goroutines and combine results.

Example:
```
func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        fmt.Printf("Worker %d processing job %d\n", id, j)
        results <- j * 2
    }
}

func main() {
    jobs := make(chan int, 5)
    results := make(chan int, 5)

    // Fan-Out: start multiple workers
    for w := 1; w <= 3; w++ {
        go worker(w, jobs, results)
    }

    // Send jobs
    for j := 1; j <= 5; j++ {
        jobs <- j
    }
    close(jobs)

    // Fan-In: collect results
    for a := 1; a <= 5; a++ {
        fmt.Println(<-results)
    }
}
```

Why: Efficiently parallelizes independent tasks.

---

### 2. Worker Pool

A variation of fan-out/fan-in.
You limit concurrency by creating a fixed number of workers.

Prevents resource exhaustion.

Good for web scraping, database queries, etc.
```

const numWorkers = 4

func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        time.Sleep(time.Second)
        results <- j * j
    }
}
```
---

### 3. Pipeline Pattern

Data flows through a series of stages, each running in its own goroutine and connected by channels.

```
func gen(nums ...int) <-chan int {
    out := make(chan int)
    go func() {
        for _, n := range nums {
            out <- n
        }
        close(out)
    }()
    return out
}

func sq(in <-chan int) <-chan int {
    out := make(chan int)
    go func() {
        for n := range in {
            out <- n * n
        }
        close(out)
    }()
    return out
}

func main() {
    in := gen(2, 3, 4)
    out := sq(in)

    for n := range out {
        fmt.Println(n)
    }
}
```


Why: Makes code modular and easy to extend (like Unix pipes).

---

### 4. Publish–Subscribe (Pub/Sub)

Multiple goroutines can receive messages from one producer via broadcast channels (often implemented using select or third-party libraries).

This pattern is useful for event systems.

### 5. Select Statement

select lets a goroutine wait on multiple channel operations.
```
select {
case msg := <-ch1:
    fmt.Println("Received", msg)
case msg := <-ch2:
    fmt.Println("Received", msg)
case <-time.After(2 * time.Second):
    fmt.Println("Timeout")
}
```

Why: Useful for timeouts, cancellation, or multiplexing.

---

### 6. Cancellation with Context

The context package provides structured concurrency — a way to cancel a whole tree of goroutines.
```
ctx, cancel := context.WithCancel(context.Background())
defer cancel()

go func() {
    for {
        select {
        case <-ctx.Done():
            fmt.Println("Worker stopped")
            return
        default:
            fmt.Println("Working...")
            time.Sleep(500 * time.Millisecond)
        }
    }
}()
```

Why: Prevents goroutine leaks and supports clean shutdowns.

---

### 7. Error Propagation Pattern

Use errgroup (from golang.org/x/sync/errgroup) to run multiple goroutines and collect errors.
```
var g errgroup.Group

urls := []string{"https://a.com", "https://b.com"}

for _, url := range urls {
    u := url
    g.Go(func() error {
        return fetch(u)
    })
}

if err := g.Wait(); err != nil {
    log.Fatal(err)
}

```

Why: Simplifies concurrent error handling.

---

### Best Practices

✅ Keep channels unidirectional when possible:

` func worker(in <-chan int, out chan<- int) `

✅ Always close channels on the sending side when done.

✅ Avoid sharing mutable data; communicate via channels.

✅ Use context for cancellation and timeouts.

✅ Limit concurrency with worker pools to avoid overwhelming resources.

---

### 🧭 Summary Table

| Pattern | Description | Use Case |
|----------|--------------|-----------|
| **Fan-Out / Fan-In** | Multiple workers handle jobs and combine results | Parallel processing |
| **Worker Pool** | Fixed number of workers handle queued jobs | Rate limiting, resource control |
| **Pipeline** | Data flows through a series of stages (each in its own goroutine) | Stream or staged processing |
| **Select Statement** | Wait on multiple channel operations simultaneously | Timeouts, multiplexing, event handling |
| **Context Cancellation** | Cancel or timeout groups of goroutines gracefully | API requests, background tasks, servers |
| **Errgroup** | Run multiple goroutines and collect their errors | Concurrent tasks with shared error handling |
| **Pub/Sub** | One producer broadcasts to many subscribers | Event-driven systems, messaging |
