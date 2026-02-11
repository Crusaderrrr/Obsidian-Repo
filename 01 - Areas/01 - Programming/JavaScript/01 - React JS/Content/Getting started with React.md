---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - React_JS
note type: Informational Note
---
We are gonna start our project with creating a folder and starting it with **Vite**, which is a lightweight web server that allows us to run our React applications.

Command:`npm create vite@latest`
It is gonna look like that:
![[Pasted image 20250511103857.png]]

```JavaScript
import './App.css'

function App() {
  return (
  <div>
    <p>React App</p>
    <Text />
  </div>
  )
}

function Text() {
  return (
    <div>
      <p>Some plain text</p>
    </div>
  )
}

export default App
```

This is the `app.jsx` file and it's where we gonna write our code. Here we have two components and one is using another. On the web page we will see two lines: 
- React App
- Some plain text

We can use *Props*:
```jsx
function App() {
  return (
  <div>
    <Text display="Hello World!" />
    <Text display = "Idi nahuy!"/>
  </div>
  )
}

function Text({display}) {
  return (
    <div>
      <p>{display}</p>
    </div>
  )
}
```

So, here the App function uses the props of Text function.

### Structure 
It is a good practice to make a separate folder for every API in `src` folder. And in those folders we create according files.