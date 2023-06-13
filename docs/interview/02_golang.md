---
sidebar_position: 2
---

# Golang
<details>
  <summary>Len vs Cap</summary>

In Go, `len` and `cap` are built-in functions used to work with slices and arrays. 

`len` is short for "length" and is used to determine the number of elements in a slice or the size of an array. It returns an integer value representing the number of elements currently present in the slice or array.

Example usage:
```go
numbers := []int{1, 2, 3, 4, 5}
fmt.Println(len(numbers)) // Output: 5

names := [3]string{"Alice", "Bob", "Charlie"}
fmt.Println(len(names)) // Output: 3
```

On the other hand, `cap` is short for "capacity" and is used specifically with slices. It returns the maximum number of elements that the slice can hold before it needs to be resized. The capacity is determined by the underlying array that the slice is referencing.

Example usage:
```go
numbers := make([]int, 5, 10)
fmt.Println(cap(numbers)) // Output: 10

names := []string{"Alice", "Bob", "Charlie"}
fmt.Println(cap(names)) // Output: 3 (same as len, as it's the initial capacity)
```

Note that for arrays, the `cap` function is not applicable as the capacity is fixed and determined by the array's length.

It's important to understand the difference between `len` and `cap` because when you append elements to a slice and its length exceeds its capacity, the underlying array will need to be resized, which can incur a performance cost.
</details>

--- 

<details>
  <summary>Empty interface</summary>

In Go, an empty interface is represented by the `interface{}` type. It is a special interface type that doesn't specify any methods. This means that any value in Go can be assigned to an empty interface.

The empty interface is used when you want to work with values of unknown type or when you need to store values of different types in a single container. Since every type in Go implements at least zero methods, an empty interface can hold values of any type.

Here's an example to illustrate the usage of an empty interface:

```go
func printValue(v interface{}) {
    fmt.Println("Value:", v)
}

func main() {
    printValue(42)          // Value: 42
    printValue("Hello")     // Value: Hello
    printValue(3.14)        // Value: 3.14
    printValue([]int{1, 2}) // Value: [1 2]
}
```

In the example above, the `printValue` function takes an empty interface parameter `v`. This means it can accept values of any type. Inside the function, the value is printed without knowing its specific type.

However, when working with an empty interface, keep in mind that you lose type safety. You won't be able to use the value in a type-specific manner unless you perform type assertions or type switches to determine the underlying type.
</details>

---

<details>
  <summary> (@TODO)Garbage collection (esacpe analysis)</summary>
  
</details>

---


