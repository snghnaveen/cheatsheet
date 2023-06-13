---
sidebar_position: 2
---

# Create a ticker

In this example, we create a new ticker using time.NewTicker, specifying a duration of 1 second. We then start a Goroutine that listens to the ticker.C channel, which will receive a value every time the ticker fires. Inside the Goroutine, we perform the desired action, which in this case is printing a message.

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	t := time.NewTicker(time.Second * 1)
	done := make(chan bool)

	go func() {
		for {
			select {
			case <-done:
				return
			case i := <-t.C:
				fmt.Println("Time is : ", i.String())
			}
		}
	}()

	time.Sleep(10 * time.Second)
	t.Stop()
	done <- true

	fmt.Println("***Done***")
}
```