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