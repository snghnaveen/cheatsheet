---
sidebar_position: 7
---

# Directional Channel

In Go, channels can be defined as either unidirectional or bidirectional, allowing you to specify the permitted operations on the channel. This distinction helps enforce the correct usage of channels and provides additional type safety.

Here's how you can define directional channels in Go:

```go
package main

import (
	"fmt"
)

func main() {
	ch := make(chan int)
	done := make(chan struct{})
	go read(ch, done)
	go write(ch)

	<-done
}

func write(ch chan<- int) {
	// <-ch invalid operation: cannot receive from send-only channel ch

	for i := 1; i <= 10; i++ {
		ch <- i // Send Only
	}
	close(ch)
}

func read(ch <-chan int, done chan<- struct{}) {
	// ch <- 1 invalid operation: cannot send to receive-only channel ch

	for {
		select {
		case v, ok := <-ch: //Receive Only
			if ok {
				fmt.Println(v)
			} else {
				done <- struct{}{}
				return
			}
		}
	}
}
```