# recoil-demo

旧版本
```js
import React, { createContext, useContext, useState } from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import reportWebVitals from './reportWebVitals';

const MyContext = createContext()

function App () {
  const [todoList, setTodoList] = useState([])
  return (
    <MyContext.Provider value={{todoList, setTodoList}}>
      <TodoApp />
    </MyContext.Provider>
  )
}

function TodoApp () {
  const { todoList, setTodoList } = useContext(MyContext)
  const [text, setText] = useState('')
  const handleInput = (e) => {
    setText(e.target.value)
  }
  const addTodo = (e) => {
    setTodoList([...todoList, text])
  }
  return (
    <div>
      <input value={text} type="text" onInput={handleInput} />
      <button onClick={() => addTodo(text)}>添加</button>
      <ul>
        {
          todoList.map(item => <li key={item}>{item}</li>)
        }
      </ul>
    </div>
  )
}

ReactDOM.render(<App />,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```
新版本
```js
import React, { createContext, useContext, useState } from 'react';
import ReactDOM from 'react-dom';
import './index.css';
// import App from './App';
import reportWebVitals from './reportWebVitals';
import { RecoilRoot, atom, useRecoilState } from 'recoil';

const todoListState = atom({
  key: 'todoList',
  default: [],
})

function App () {
  return (
    <RecoilRoot>
      <TodoApp />
    </RecoilRoot>
  )
}

function TodoApp () {
  const [ todoList, setTodoList ] = useRecoilState(todoListState)
  const [text, setText] = useState('')
  const handleInput = (e) => {
    setText(e.target.value)
  }
  const addTodo = (e) => {
    setTodoList([...todoList, text])
  }
  return (
    <div>
      <input value={text} type="text" onInput={handleInput} />
      <button onClick={() => addTodo(text)}>添加</button>
      <ul>
        {
          todoList.map(item => <li key={item}>{item}</li>)
        }
      </ul>
    </div>
  )
}

ReactDOM.render(<App />,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```