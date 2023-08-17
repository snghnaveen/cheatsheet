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