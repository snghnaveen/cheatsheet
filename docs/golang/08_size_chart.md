---
sidebar_position: 8
---

# Size Chart

| Data Type      | Size (bytes)              | Notes                                                                      |
| -------------- | ------------------------- | -------------------------------------------------------------------------- |
| **bool**       | 1                         | Can store `true` or `false`                                                |
| **int**        | 8                         | Size depends on system architecture (4 bytes on 32-bit, 8 bytes on 64-bit) |
| **int8**       | 1                         | Range: -128 to 127                                                         |
| **int16**      | 2                         | Range: -32,768 to 32,767                                                   |
| **int32**      | 4                         | Range: -2,147,483,648 to 2,147,483,647                                     |
| **int64**      | 8                         | Range: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807             |
| **uint**       | 8                         | Depends on system architecture (4 bytes on 32-bit, 8 bytes on 64-bit)      |
| **uint8**      | 1                         | Range: 0 to 255                                                            |
| **uint16**     | 2                         | Range: 0 to 65,535                                                         |
| **uint32**     | 4                         | Range: 0 to 4,294,967,295                                                  |
| **uint64**     | 8                         | Range: 0 to 18,446,744,073,709,551,615                                     |
| **float32**    | 4                         | IEEE-754 single-precision floating point                                   |
| **float64**    | 8                         | IEEE-754 double-precision floating point                                   |
| **complex64**  | 8                         | 32-bit real and 32-bit imaginary                                           |
| **complex128** | 16                        | 64-bit real and 64-bit imaginary                                           |
| **byte**       | 1                         | Alias for `uint8`                                                          |
| **rune**       | 4                         | Alias for `int32`, used for Unicode code points                            |
| **string**     | 16 + length               | 16 bytes for overhead, plus 1 byte per character                           |
| **array**      | Size of elements × length | Fixed size, depends on type of elements                                    |
| **slice**      | 24                        | 8 bytes for pointer, 8 bytes for length, 8 bytes for capacity              |
| **map**        | Varies                    | Depends on number of entries and type of keys and values                   |
| **channel**    | 8                         | Pointer to the channel                                                     |
| **struct**     | Sum of field sizes        | Size depends on fields, includes padding for alignment                     |
| **pointer**    | 8                         | 8 bytes on a 64-bit system, 4 bytes on 32-bit                              |


### Go code to print the sizes of the types listed in your table, using `unsafe.Sizeof()` :

```go

package main

import (
	"fmt"
	"unsafe"
)

func main() {
	fmt.Printf("Size of bool: %d bytes\n", unsafe.Sizeof(true)) // bool
	fmt.Printf("Size of int: %d bytes\n", unsafe.Sizeof(int(0))) // int
	fmt.Printf("Size of int8: %d bytes\n", unsafe.Sizeof(int8(0))) // int8
	fmt.Printf("Size of int16: %d bytes\n", unsafe.Sizeof(int16(0))) // int16
	fmt.Printf("Size of int32: %d bytes\n", unsafe.Sizeof(int32(0))) // int32
	fmt.Printf("Size of int64: %d bytes\n", unsafe.Sizeof(int64(0))) // int64
	fmt.Printf("Size of uint: %d bytes\n", unsafe.Sizeof(uint(0))) // uint
	fmt.Printf("Size of uint8: %d bytes\n", unsafe.Sizeof(uint8(0))) // uint8
	fmt.Printf("Size of uint16: %d bytes\n", unsafe.Sizeof(uint16(0))) // uint16
	fmt.Printf("Size of uint32: %d bytes\n", unsafe.Sizeof(uint32(0))) // uint32
	fmt.Printf("Size of uint64: %d bytes\n", unsafe.Sizeof(uint64(0))) // uint64
	fmt.Printf("Size of float32: %d bytes\n", unsafe.Sizeof(float32(0))) // float32
	fmt.Printf("Size of float64: %d bytes\n", unsafe.Sizeof(float64(0))) // float64
	fmt.Printf("Size of complex64: %d bytes\n", unsafe.Sizeof(complex64(0))) // complex64
	fmt.Printf("Size of complex128: %d bytes\n", unsafe.Sizeof(complex128(0))) // complex128
	fmt.Printf("Size of byte: %d bytes\n", unsafe.Sizeof(byte(0))) // byte (alias for uint8)
	fmt.Printf("Size of rune: %d bytes\n", unsafe.Sizeof('a')) // rune (alias for int32)
	fmt.Printf("Size of string: %d bytes\n", unsafe.Sizeof("")) // string (empty string, size of overhead)
	
	// Array: Fixed-size array (of 4 int32 elements)
	var arr [4]int32
	fmt.Printf("Size of array (4 * int32): %d bytes\n", unsafe.Sizeof(arr)) // array of 4 int32 elements

	// Slice: Dynamic-size slice
	var slice []int32
	fmt.Printf("Size of slice: %d bytes\n", unsafe.Sizeof(slice)) // slice (pointer, length, capacity)

	// Map: Maps memory size may vary based on entries and types
	var m map[int]int
	fmt.Printf("Size of map: %d bytes\n", unsafe.Sizeof(m)) // map (pointer)

	// Channel: A channel for int values
	var ch chan int
	fmt.Printf("Size of channel: %d bytes\n", unsafe.Sizeof(ch)) // channel (pointer)

	// Struct: Example of a struct with padding
	type Example struct {
		b bool   // 1 byte
		i int64  // 8 bytes
		f float32 // 4 bytes
	}
	var s Example
	fmt.Printf("Size of struct (Example): %d bytes\n", unsafe.Sizeof(s)) // struct (with padding)
	
	// Pointer: Size of a pointer to an int
	var p *int
	fmt.Printf("Size of pointer: %d bytes\n", unsafe.Sizeof(p)) // pointer (platform-dependent)
}

```

---

### Expected Output (on a 64-bit system):
```bash
Size of bool: 1 bytes
Size of int: 8 bytes
Size of int8: 1 bytes
Size of int16: 2 bytes
Size of int32: 4 bytes
Size of int64: 8 bytes
Size of uint: 8 bytes
Size of uint8: 1 bytes
Size of uint16: 2 bytes
Size of uint32: 4 bytes
Size of uint64: 8 bytes
Size of float32: 4 bytes
Size of float64: 8 bytes
Size of complex64: 8 bytes
Size of complex128: 16 bytes
Size of byte: 1 bytes
Size of rune: 4 bytes
Size of string: 16 bytes
Size of array (4 * int32): 16 bytes
Size of slice: 24 bytes
Size of map: 8 bytes
Size of channel: 8 bytes
Size of struct (Example): 24 bytes
Size of pointer: 8 bytes
```

---

#### Note :
- bool, int8, uint8, byte, rune: These types are small fixed sizes.
- int, uint, int64, uint64, pointer: These types are platform-dependent. On 64-bit systems, they are typically 8 bytes.
- array: The size is based on the number of elements and their size.
- slice: Always 24 bytes, as it stores a pointer, a length, and a capacity.
- map and channel: Their size is 8 bytes (on 64-bit) since they store a pointer to the data structure.
- string: The overhead of a string is always 16 bytes, not counting the actual string content.
- struct: The size includes padding for alignment.
