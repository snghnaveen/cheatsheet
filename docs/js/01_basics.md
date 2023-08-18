---
sidebar_position: 1
---

# Basics

### Class and constructor 
```js
class Rectangle {
    constructor(l, b){
        this.l = l;
        this.b = b;
    }
    
    area(){
        return this.l * this.b;
    }
}

var rect = new Rectangle(10,2);
console.log(rect.area());
```

### Map and Array

```js
const hobbies = ["Sports", "Cooking", "Reading"];

console.log(hobbies[1]); // Cooking
hobbies.push("Painting")

const idx = hobbies.findIndex((item) => {
    return item === "Sports";
})

// OR

const idx2 = hobbies.findIndex((item) => item === "Sports")

console.log(idx, idx2); // 0 0

const editedHobbies = hobbies.map((item) => item + "!");

console.log(editedHobbies[1]); // Cooking!

const objHobbies = hobbies.map((item) => ({text : item}))
console.log(objHobbies[1]); // { text: 'Cooking' }
```

### Destructuring 
```js
const name = ["naveen", "singh"];

// const fName = name[0];
// const lName = name[1];
// console.log(fName, lName); // naveen singh

const [fname, lname] = name;
console.log(fname, lname); // naveen singh


const usr = {
    name : "snghnaveen",
    age: 45
}

// name = usr.name
// age = usr.age

const {name: Username, age} = usr
console.log(Username, age) // snghnaveen
```

### Spread Operator

```js
hobbies = ["Sports", "Music", "Painting"];
moreHobbies = ["Reading"];

mergedHobbies = [...hobbies, ...moreHobbies];
console.log(mergedHobbies) // [ 'Sports', 'Music', 'Painting', 'Reading' ]


const usr = {
    name : "nav",
    age : 28
}

const extUsr = {
    gender : "male",
    ...usr
}

console.log(extUsr); // { gender: 'male', name: 'nav', age: 28 }
```

### Array functions
- reduce
  ```js
     const message = ["JavaScript ", "is ", "not ", "fun."];
    // function to join each string elements
    function joinStrings(accumulator, currentValue) {
      console.log("accumulator", accumulator, "currentValue",currentValue);
    // accumulator JavaScript  currentValue is 
    // accumulator JavaScript is  currentValue not 
    // accumulator JavaScript is not  currentValue fun.
      return accumulator + currentValue;
    }
    
    // reduce join each element of the string
    let joinedString = message.reduce(joinStrings);
    console.log(joinedString); // JavaScript is not fun.
  ```

- splice
  ```js
    const months = ['Jan', 'March', 'April', 'June'];
    months.splice(1, 0, 'Feb');
    // Inserts at index 1
    console.log(months);
    // Expected output: Array ["Jan", "Feb", "March", "April", "June"]
    
    months.splice(4, 1, 'May');
    // Replaces 1 element at index 4
    console.log(months);
    // Expected output: Array ["Jan", "Feb", "March", "April", "May"]
  ```

- slice
  ```js
    const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

    console.log(animals.slice(2));
    // Expected output: Array ["camel", "duck", "elephant"]
    
    console.log(animals.slice(2, 4));
    // Expected output: Array ["camel", "duck"]
    
    console.log(animals.slice(1, 5));
    // Expected output: Array ["bison", "camel", "duck", "elephant"]
    
    console.log(animals.slice(-2));
    // Expected output: Array ["duck", "elephant"]
    
    console.log(animals.slice(2, -1));
    // Expected output: Array ["camel", "duck"]
    
    console.log(animals.slice());
    // Expected output: Array ["ant", "bison", "camel", "duck", "elephant"]
  ```
