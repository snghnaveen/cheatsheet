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
  <summary> Understanding Allocations: the Stack and the Heap </summary>
  https://www.youtube.com/watch?v=ZMZpH4yT7M0
</details>

---

<details>
  <summary> Shallow Copy vs Deep Copy </summary>
  In Go, a deep copy and a shallow copy are two different ways of copying data from one variable to another. Let's understand the concepts with an example:

  ```go
  package main

  import (
    "fmt"
  )

  type Person struct {
    Name string
    Age  int
  }

  func main() {
    // Creating an instance of the Person struct
    person1 := Person{Name: "John", Age: 30}

    // Shallow copy
    person2 := person1

    // Deep copy
    person3 := Person{Name: person1.Name, Age: person1.Age}

    // Modifying the original object
    person1.Name = "Alice"
    person1.Age = 25

    // Printing the copied objects
    fmt.Println("Shallow Copy:", person2.Name, person2.Age)
    fmt.Println("Deep Copy:", person3.Name, person3.Age)
  }
  ```

  In the above code, we have a `Person` struct with two fields: `Name` and `Age`. We create an instance of the struct named `person1` with name "John" and age 30.

  1. Shallow Copy:
    Shallow copying creates a new variable, `person2`, and copies the memory address of the original object. The fields of `person2` will point to the same memory locations as `person1`. Changes made to the original object will be reflected in the copied object, and vice versa.

  2. Deep Copy:
    Deep copying creates a completely new variable, `person3`, and copies the values of the fields from the original object into the new object. Changes made to the original object will not affect the copied object, and vice versa.

  In the example, we modify the `Name` and `Age` fields of `person1` after copying. When we print the copied objects `person2` and `person3`, we can observe the following:

  ```
  Shallow Copy: Alice 25
  Deep Copy: John 30
  ```

  As you can see, the shallow copy reflects the changes made to the original object, while the deep copy retains the original values.  

</details>

---

<details>
  <summary> Pass by value vs Pass by reference </summary>
  In Go, all function arguments are passed by value by default. However, Go also provides a mechanism to pass arguments by reference using pointers. Let's explore both concepts: pass by value and pass by reference in Go.

1. Pass by Value:
   When you pass an argument by value, a copy of the value is created and passed to the function. Any modifications made to the parameter inside the function do not affect the original value outside the function.

   Example:

   ```go
   package main

   import "fmt"

   func modifyValue(num int) {
       num = 10 // Modifying the local copy
   }

   func main() {
       num := 5
       modifyValue(num)
       fmt.Println(num) // Output: 5 (original value remains unchanged)
   }
   ```

   In the example above, the `modifyValue` function receives `num` as an argument, but any changes made to `num` inside the function do not affect the original value in the `main` function.

2. Pass by Reference (using Pointers):
   Go supports pointers, which allow you to pass arguments by reference. A pointer stores the memory address of a value rather than the value itself. By passing a pointer to a function, you can modify the original value directly.

   Example:

   ```go
   package main

   import "fmt"

   func modifyValueByReference(num *int) {
       *num = 10 // Modifying the original value through the pointer
   }

   func main() {
       num := 5
       modifyValueByReference(&num)
       fmt.Println(num) // Output: 10 (original value is modified)
   }
   ```

   In the example above, the `modifyValueByReference` function takes a pointer to an integer (`*int`) as an argument. By dereferencing the pointer using the `*` operator, we can modify the original value directly.

   Note that when passing a pointer to a function, you need to use the `&` operator before the variable name to get its address.

It's important to understand the difference between pass by value and pass by reference because it affects how modifications to function arguments behave. Most arguments in Go are passed by value to avoid unintentional side effects. However, using pointers allows you to explicitly pass arguments by reference and modify the original values if needed.
</details>

---

<details>
  <summary> Is slice pass by value?  </summary>
  In Go, slices are actually a reference type, so when you pass a slice to a function, it is passed by value, but the underlying data structure it refers to is not copied. This means that modifications made to the elements of a slice within a function will be reflected in the original slice.

Let's see an example to better understand this behavior:

```go
package main

import "fmt"

func modifySlice(slice []int) {
    slice[0] = 10 // Modifying the first element of the slice
    slice = append(slice, 4) // Appending a new element to the slice
}

func main() {
    originalSlice := []int{1, 2, 3}
    modifySlice(originalSlice)
    fmt.Println(originalSlice) // Output: [10 2 3] (modified first element)
}
```

In the example above, we have a `modifySlice` function that takes a slice as an argument. Inside the function, we modify the first element of the slice to 10. When we print the `originalSlice` in the `main` function after calling `modifySlice`, we can see that the change made inside the function is reflected in the original slice.

However, when we append a new element to the slice inside the `modifySlice` function, it doesn't affect the original slice. This is because appending a new element may require allocating new memory if the underlying array is full, and in that case, the reference to the slice would be different inside the function.

To summarize, slices are passed by value in Go, but since they hold a reference to the underlying array, modifications to the elements of the slice will be visible outside the function. Just be aware that modifying the structure of the slice itself (e.g., appending elements) might not affect the original slice if a reallocation is needed.
</details>


---

<details>
  <summary> Explain Closure </summary>
  In Go, closures are a powerful feature that allows you to create anonymous functions that can access and manipulate variables defined outside their body. A closure binds the variables it references, ensuring their availability even after the surrounding function has finished executing.

Here's an example to illustrate closures in Go:

```go
package main

import "fmt"

func main() {
	// Outer function that returns a closure
	generator := generateNumbers()

	// Use the closure to generate numbers
	fmt.Println(generator()) // Output: 1
	fmt.Println(generator()) // Output: 2
	fmt.Println(generator()) // Output: 3
}

// Outer function that returns a closure
func generateNumbers() func() int {
	// Variable defined outside the closure
	count := 0

	// Inner closure function
	return func() int {
		count++
		return count
	}
}
```

In the example above, we have an outer function `generateNumbers()` that returns a closure. The closure is an anonymous function that increments a variable `count` defined outside its body. 

In the `main()` function, we create an instance of the closure by assigning the result of `generateNumbers()` to the `generator` variable. We can then use the `generator` closure to generate a sequence of numbers. Each time we invoke `generator()`, the `count` variable is incremented and its updated value is returned.

When we run the program, we get the output:

```
1
2
3
```

The closure maintains the state of the `count` variable between function calls, even though `generateNumbers()` has already returned. This is the behavior of closures in Go, where they capture and preserve the environment in which they were defined.

Closures are often used in Go for encapsulating functionality, creating iterators, and implementing callbacks. They provide a way to define and use functions inline without the need for explicit function declarations.
</details>


<!-- 
<details>
  <summary> Heading  </summary>
  Answer
</details> -->