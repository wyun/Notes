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

## Mapping Components

When we have an array, we can use Array.map to generate JSX array. Then this JSX array can be used directly in {} and be interprated by React properly.

## Class-based component

convert functional component to class based component

Every class based component must have a `render` method.

For `props`, remember to use `this.props` inside the class.

We can abbreviate `extends React.Component` to `extends Component`, if the top import statement is changed to `import React, {Component} from 'react'`

```JS

// function App() {
//     return (
//         <div>
//             <h1>Code goes here</h1>
//         </div>
//     )
// }

class App extends React.Component {

    yourMethodHere() {

    }

    render() {
        // add other display logic and your own methods. Call your own method with `this.yourMethod`
        const style = this.yourMethodHere()

        const date = new Date()
        return (
            <div>
                <h1>Code goes here {date.getFullYear()}</h1>
                {this.props.whatever}
            </div>
        )
    }
}

```

## State

`props` are immutible.

`state` is mutable. Whenever `state` is needed, we will need to use `class-based component`

`constructor` method is a special method in JS to initialize part of the component. More information about ES6 class, [tutorial](ttps://scrimba.com/p/p4Mrt9/cQnMDHD). `super()` should always be called first inside, to get the parent/super class's goodies.

```JS
class App extends React.Component {
    constructor() {
        super()
        this.state = {}
    }

    render() {
        return (

        )
    }
}
```

## Handling Events

camelCased event handlers:

- onClick
- onMouseOver

```JS
    return (
        <button onClick="myFunction()">Click me</button>
    )
```

## Changing State

Do not change `this.state` directly. Use `this.setState()` instead.

One caveat:

- Anytime when you want to use a customized method, you need to use `bind` to bind it to its own class.

When changing based on previous state, pass in prevState, then return a new object.

```JS
    class App extends Component {
        constructor() {
            super()
            this.state = {count: 0}
            // this following line is important to expose `this` to that method
            this.handleClick = this.handleClick.bind(this)
        }

        handleClick() {
            this.setState(prevState => {
                return {
                    count: prevState.count + 1
                }
            })
        }
        
        render() {
            return (
                <div>
                    <h1>{this.state.count}</h1>
                    <button onClick={this.handleClick}>Change!</button>
                </div>
            )
        }
    }
```

## React Lifecycle Methods

[Explaination of lifecycles before 16.3](https://engineering.musefind.com/react-lifecycle-methods-how-and-when-to-use-them-2111a1b692b1)

[Lifecycles after 16.3](https://reactjs.org/blog/2018/03/29/react-v-16-3.html#component-lifecycle-changes) or [another link](https://blog.bitsrc.io/react-16-lifecycle-methods-how-and-when-to-use-them-f4ad31fb2282)

Lifcecycle Methods:

- `componentDidMount()`: only run once when component is on screen. Most often, it is used to call an API to get information.
- `componentWillReceiveProps(nextProps)`: will run whenever a parent component decides to pass down props. This method is deprecated. 
- `shouldComponentUpdate(nextProps, nextState)`: gives developer to change the default updating behavior and make component more performant. return true if want update; return false if not.
- `componentWillUnmount()`: do some clean up or tear down in the DOM or application, remove event listener, before component disappears.