---
sidebar_position: 1
---

# Recover a panic

In this example, we use the defer statement to schedule the recovery code to be executed when the function returns. Inside the deferred function, we call recover() to capture the panic value.

```go
package main

import "fmt"

func main() {
  // Recover example
	process()
}

func process() {
	defer func() {
		if r := recover(); r != nil {
			fmt.Println("Recovered in process:", r)
		}
	}()
	doWork()
}

func doWork() int {
	panic("I can't do this!!!")
}
```