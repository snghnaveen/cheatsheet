---
sidebar_position: 1
---

# Class and constructor

Class and constructor 
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