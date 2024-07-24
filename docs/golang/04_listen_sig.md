---
sidebar_position: 4
---

# Listen to OS signals (Ctrl+C to exit)

In this example , we create a channel called signalChannel to receive OS signals. We then use signal.Notify to notify the channel when an interrupt (Ctrl+C) or termination signal (SIGTERM) is received.

The program will block at `<-` signalChannel, waiting for a signal to be received. Once a signal is received, it will continue executing, and you can handle the signal as needed. In the example, we simply print a message and exit the program, but you can perform any cleanup or necessary actions before exiting.

```go
package main

import (
	"fmt"
	"os"
	"os/signal"
	"syscall"
	"time"
)

func main() {
	// Create a channel to receive OS signals
	signalChannel := make(chan os.Signal, 1)

	// Notify the channel when an interrupt or termination signal is received
	signal.Notify(signalChannel, os.Interrupt, syscall.SIGTERM)

	fmt.Println("Press Ctrl+C to exit.")

	go func() {
		<-signalChannel
		// cleanup()
		fmt.Println("exiting gracefully...")
		os.Exit(0)

	}()

	// app running
	for {
		time.Sleep(time.Second * 10)
	}

}
```