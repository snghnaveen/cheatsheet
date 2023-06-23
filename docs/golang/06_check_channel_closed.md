---
sidebar_position: 5
---

# Check channel is closed
In Go, you can check if a channel is closed or not using a combination of a select statement and an additional boolean variable. Here's an example:

```go
package main

import "fmt"

func main() {
	ch := make(chan int)

	// Close the channel after some time
	go func() {
		defer close(ch)
		for i := 1; i <= 5; i++ {
			ch <- i
		}
	}()

	for {
		// Check if the channel is closed
		val, ok := <-ch
		if !ok {
			fmt.Println("Channel closed")
			break
		}
		fmt.Println("Received:", val)
	}
}
```
