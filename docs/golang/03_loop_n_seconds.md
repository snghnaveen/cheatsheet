---
sidebar_position: 3
---

# Loop n seconds

In this example, we specify the number of seconds we want to loop until with the variable n.

To loop until a certain number of seconds have passed in Go, you can use the time package and the time.After function. Here's an example:

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	i := 0
	n := 15
	for timeout := time.Now().Add(n * time.Second); timeout.After(time.Now()); {
		i++
		fmt.Println("Second : ", i)
		time.Sleep(1 * time.Second)
	}
}
```