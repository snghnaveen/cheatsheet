---
sidebar_position: 3
---

# Loop n seconds

To loop until a certain number of seconds have passed in Go, you can use the time package and the time.After function. Here's an example:

In this example, we specify the number of seconds we want to loop until with the variable n. We get the current time using time.Now(). Then, we calculate the target time by adding n seconds to the start time using start.Add(time.Duration(n) * time.Second).

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