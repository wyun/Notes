# Learning React

[Playlist](https://scrimba.com/playlist/p7P5Hd)

## Introduction

HTML CSS JS ES6
Props State
[Virtual DOM](https://www.youtube.com/watch?v=BYbgopx44vo)

[My Code](https://codepen.io/ovdcp/pen/mgmYJg)

## ReactDOM & JSX

The first thing to do in every React app is to:
- import react
- import react-dom
Add react-dom and react dependencies first, then
```JS
// index.js
import React from "react"
import ReactDOM from "react-dom"

//ReactDOM.render(WHAT DO I WANT TO RENDER in JSX, WHERE DO I WANT TO RENDER IT as DOM node)
ReactDOM.render(<h1>Hello World!</h1>, document.getElementById("root"))
```

## Functional Components

Simply return the JSX from MyApp function, then call `<MyApp />` as JSX in `ReactDOM.render()`. 

JSX must be one single element. You can always wrap around a `div` if necessary. 

```JS
function MyApp() {
    return (
        <ul>
            <li>A</li>
            <li>B</li>
            <li>C</li>
        </ul>
    )
}

ReactDOM.render(
    <MyApp />,
    document.getElementById('root')
);
```

## Move components into Separate files
1. Move MyInfo() to a different file and call it 'MyInfo.js'. Make sure to add react import statement. Almost every react component need that line
2. Export it in the end to make it available to other applications. 
3. Import it in the main file where it is used. `import MyInfo from "./MyInfo"`. Relative path and file name is needed. Default is 'js' extension. So it can be omitted.

```JS
import React from "react"

function MyInfo() {
  return (
    <div>
      <h1>Bob Ziroll</h1>
    </div>
  )
}

export default MyInfo
```

To understand more about ES6's import and export statements. Scrimba has a course on it.


## Parent/Child Components

When creating components, almost capitlize the first character, so we can easily distinguish a regular html element from a React component.

Semantic HTML5 elements
- header
- nav
- main
- footer

## Styling React

- with Class: in JSX, we cannot add `class` to an element, we must use `className`. `className` can only be applied to elements, not user created components. 
- with inline style: only style object can be used, not typical string: `<h1 style={{color: "red"}}>Good morning</h1>` The inner set of curly braces is for object itself, the outer set of curly braces is to tell that it's javascript, so that JSX can interpret it as such. Propery names need to be camelCase, such as `backgroundColor`

Here is some basic CSS to get a project started. 

```CSS
body {
    margin: 0;
}

.navbar {
    height: 100px;
    background-color: #333;
    color: whitesmoke;
    margin-bottom: 15px;
    text-align: center;
    font-size: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
}

```

In JSX, access to Javascript variables and constants can be accessed through a pair of `{ }`. we can use ES6 string template to access variables with ${varName}

```JS
const firstName = "John"
const lastName = "Doe"

return (
    <h1>Hello, {`${firstName} ${lastName}`}!</h1>
)
```

## Props

Attribute in html sense. Access props using `props.propName`
```JSX
<ContactCard name="John Doe" imgUrl="" age="36" />
```

```JS
function ContactCard(props) {
    return (
        <div className="contact-card">
            <h3>{props.name}</h3>
            <p>Age: {props.age}</p>
        </div>
    )
}
```

We can also pass in object. 
```JSX
<ContactCard contact={{
    name: "John Doe",
    age: "36"
}} />
```

If a property is not defined in JSX, that property will be null. 