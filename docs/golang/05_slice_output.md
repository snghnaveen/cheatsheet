---
sidebar_position: 5
---

# Slice output

This example will help to directly see the behavior of various slice operations.

```go
package main

import "fmt"

type Slc struct {
	A, B, C []int
}

func (s *Slc) Print(logName string) {
	fmt.Println(logName, "-")
	fmt.Println("A", ":", s.A, " | len", len(s.A), " | cap", cap(s.A))
	fmt.Println("B", ":", s.B, "| len", len(s.B), "| cap", cap(s.B))
	fmt.Println("C", ":", s.C, "| len", len(s.C), "| cap", cap(s.C))
	fmt.Println()
}

func main() {
	slc := Slc{
		A: []int{1, 2},
		B: []int{3, 4},
	}
	slc.Print("initial")

	slc.C = slc.A
	slc.Print("after setting A to C")

	slc.A[0] = 12
	slc.Print("after setting A[0] to 12")

	copy(slc.A, slc.B)
	slc.Print("after copy B to C")

	slc.A[0] = 14
	slc.Print("after setting A[0] to 14")

	slc.A[0] = 15
	slc.Print("after setting C[0] to 15")

	slc.B[0] = 11
	slc.Print("after setting B[0] to 11")

	// When we append 5 to A, a new array is created
	slc.A = append(slc.A, 5)
	slc.Print("after appending 5 to A")

	slc.A[0] = 10
	slc.Print("after setting A[0] to 10")

	slc.A = slc.A[:1]
	slc.Print("after setting A to slc.A[:1]")

	slc.A = []int{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	slc.Print("after setting A to {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}")

	slc.A = slc.A[0:len(slc.A)]
	slc.Print("after setting A to slc.A[0:len(slc.A)]")

	slc.A = slc.A[0:5]
	slc.Print("after setting A to slc.A[0:5]")

	slc.A = slc.A[2:4]
	slc.Print("after setting A to slc.A[2:4]")
}

```

Output :

```sh
initial -
A : [1 2]  | len 2  | cap 2
B : [3 4] | len 2 | cap 2
C : [] | len 0 | cap 0

after setting A to C -
A : [1 2]  | len 2  | cap 2
B : [3 4] | len 2 | cap 2
C : [1 2] | len 2 | cap 2

after setting A[0] to 12 -
A : [12 2]  | len 2  | cap 2
B : [3 4] | len 2 | cap 2
C : [12 2] | len 2 | cap 2

after copy B to C -
A : [3 4]  | len 2  | cap 2
B : [3 4] | len 2 | cap 2
C : [3 4] | len 2 | cap 2

after setting A[0] to 14 -
A : [14 4]  | len 2  | cap 2
B : [3 4] | len 2 | cap 2
C : [14 4] | len 2 | cap 2

after setting C[0] to 15 -
A : [15 4]  | len 2  | cap 2
B : [3 4] | len 2 | cap 2
C : [15 4] | len 2 | cap 2

after setting B[0] to 11 -
A : [15 4]  | len 2  | cap 2
B : [11 4] | len 2 | cap 2
C : [15 4] | len 2 | cap 2

after appending 5 to A -
A : [15 4 5]  | len 3  | cap 4
B : [11 4] | len 2 | cap 2
C : [15 4] | len 2 | cap 2

after setting A[0] to 10 -
A : [10 4 5]  | len 3  | cap 4
B : [11 4] | len 2 | cap 2
C : [15 4] | len 2 | cap 2

after setting A to slc.A[:1] -
A : [10]  | len 1  | cap 4
B : [11 4] | len 2 | cap 2
C : [15 4] | len 2 | cap 2

after setting A to {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10} -
A : [0 1 2 3 4 5 6 7 8 9 10]  | len 11  | cap 11
B : [11 4] | len 2 | cap 2
C : [15 4] | len 2 | cap 2

after setting A to slc.A[0:len(slc.A)] -
A : [0 1 2 3 4 5 6 7 8 9 10]  | len 11  | cap 11
B : [11 4] | len 2 | cap 2
C : [15 4] | len 2 | cap 2

after setting A to slc.A[0:5] -
A : [0 1 2 3 4]  | len 5  | cap 11
B : [11 4] | len 2 | cap 2
C : [15 4] | len 2 | cap 2

after setting A to slc.A[2:4] -
A : [2 3]  | len 2  | cap 9
B : [11 4] | len 2 | cap 2
C : [15 4] | len 2 | cap 2
```