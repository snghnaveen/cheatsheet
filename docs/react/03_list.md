---
sidebar_position: 3
---
# List

- Render list dynamically
```jsx
const DUMMY_TODOS = [
  'Learn React',
  'Practice React',
  'Profit!'
];


export function App(props) {
  return (
    <div className='App'>
        {DUMMY_TODOS.map(item =>  <ul>{item}</ul>)}
    </div>
  );
}
```

- Add to list dynamically
```jsx

const DUMMY_TODOS = [
  {
    id : 'ecpwi3',
    val : 'qb9lk'
  },
  {
    id : 'j81w2',
    val : 'j81w2'
  },
  {
    id : '22olq',
    val : '22olq'
  }
];

export default function App(props) {
  const [todo, setTodos] = useState(DUMMY_TODOS);

  const addTodoHandler = (todo) => {
    setTodos((prevTodos) => {
      return [todo, ...prevTodos];
    });
  };

  return (
    <div>
    <MyButton onGenerate={addTodoHandler}> </MyButton>
    <Li todos={todo}></Li>
    </div>
  );
}

function Li(props) {
    return (
    <div>
        {props.todos.map(item => <ul key={item.val}>{item.val}</ul>)}
    </div>
  );
}

function MyButton(props) {
  const saveTodoHandler = () => {
    const newTodo =
    {
      id : (Math.random() + 1).toString(36).substring(7),
      val : (Math.random() + 1).toString(36).substring(7)
    } 
    props.onGenerate(newTodo);
  };

  return (
    <button onClick={saveTodoHandler}> Ok to add random row </button>
  );  
}
```

- Conditional Content
```jsx
export default function App(props) {
  const [isDeleting, setIsDeleting] = React.useState(false);
    
  function deleteHandler() {
      setIsDeleting(true);
  }

  function proceedHandler() {
      setIsDeleting(false);
  }
  
  return (
    <div>
    {isDeleting ? <div id="alert">
      <h2>Are you sure?</h2>
      <p>These changes can't be reverted!</p>
      <button onClick={proceedHandler}>Proceed</button>
    </div> : ''}
    <button onClick={deleteHandler}>Delete</button>
  </div>    
  );
}
```