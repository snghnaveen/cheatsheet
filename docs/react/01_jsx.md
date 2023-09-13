---
sidebar_position: 1
---

# JSX

### Mutiple tags  
```jsx
function ExpenseItem(){
  return (
    <div>
      <div> Date </div>
      <div> 
        <h1> Title </h1>
        <div> Amount </div>
      </div>
    </div>
  )
}

export default ExpenseItem;
```

### Pass props
```jsx
  <Concept {img={concepts[0].img} title={concepts[0].title} }></Concept>
``` 
or

```jsx
  <Concept {...concepts[0]}></Concept>
``` 

