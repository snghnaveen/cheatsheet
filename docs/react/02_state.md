---
sidebar_position: 2
---
# State

```jsx
export default function App() {
  const [price, setPrice] = React.useState(100);

  const clickHandler = () => {
    setPrice(75);
  };

  return (
    <div>
      <p>{price}</p>
      <button onClick={clickHandler}>Apply Discount</button>
    </div>
  );
}
```

### State input - Update text once input's length > 3
```jsx
export default function App() {
  const [messageValidity, setMessageValidity] = React.useState("Invalid");

  const msgHandler = () => {
    setMessage("Updated!");
    console.log(title);
  };

  function messageChangeHandler(event) {
    const value = event.target.value;
    if (value.trim().length < 3) {
      setMessageValidity("Invalid");
    } else {
      setMessageValidity("Valid");
    }
  }

  return (
    <form>
      <label>Your message</label>
      <input type="text" onChange={messageChangeHandler} />
      <p>{messageValidity} message</p>
    </form>
  );
}
```

### Update counter text
```jsx
export default function App() {
    
    const [counter, setCounter] = React.useState(0);
    
    function incrementCounterHandler() {
        setCounter(prevCounter => prevCounter + 1);
    }    
    
    return (
      <div>
        <p id="counter">{counter}</p>
        <button onClick={incrementCounterHandler}>Increment</button>
      </div>
    );
}
```


### Two way binding/ pass state from lower to upper

ExpenseFilter (lower)
```jsx
const ExpensesFilter = (pros) => {
  const dropDownChangeHandler = (event) => {
    pros.onChangeFilter(event.target.value)
  };

  return (    
    <div className='expenses-filter'>
      <div className='expenses-filter__control'>
        <label>Filter by year</label>
        <select value={pros.selected} onChange={dropDownChangeHandler}>
          <option value='2022'>2022</option>
          <option value='2021'>2021</option>
          <option value='2020'>2020</option>
          <option value='2019'>2019</option>
        </select>
      </div>
    </div>
  );
};

export default ExpensesFilter;
```

Expenses.js (upper)
```jsx
const Expenses = (props) => {

  const [filterState, setFilteredYear] = useState('2020');

  const filterChangeHandler = selectedYear => {
    console.log("ok");
    console.log(selectedYear)
    setFilteredYear(selectedYear);
  }

  return (
    <Card className="expenses">
      <ExpensesFilter selected={filterState} onChangeFilter={filterChangeHandler}/>
      <ExpenseItem
.
.
.
```