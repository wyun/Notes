# React - The Complete Guide (includes Hooks, React Router, and Redux) Second Edition [2021 Updated]

[Video Lecture on O'Reilly](https://learning.oreilly.com/videos/react-the/9781801812603/)

# HTML Primer

You can set min, max attribute to form element and let them behave properly in modern browsers. 
```html
<input type="number" name="" id="" min="0.01" step="0.01" />
<input type="date" name="" id="" min="2021-07-01" max="2022-09-01" />
```
# JavaScript Primer
[PDF notes from the author](./react_2021_images/next-gen-js-summary.pdf)
Don't use `var` .  Use `let` for variable, use `const` for constant.
## Arrow functions
No more issues with `this` keyword!  
`this` in arrow function always refers in the correct context and won't change during run time. 

Another note is the variable in ().  If there is only one variable, `()` can be ignored.  If there is none, or more than one variable, `()` is required.
```JS
    const myFunc = (name, age) => {

    }
    // with one line function, ignore {} and `return`
    const oneLineFunc = (number) => number * 2
```
## Export & Import (Modules)

![Import and Export](./react_2021_images/import_export.png)

There are two kinds of exports:
- `default` (unnamed) export: `export default ...;`
- `named` export: `export const someData = ...;`

A file can contain *only* one `default` export and unlimited `named` exports

```JS
// default export
const = person = {
    name: "Max"
}
export default person
```

```JS

export const clean = () => {...}
export const baseData = 10;
```

You can import `default exports` like this:
`import someNameOfYourChoice from './path/to/file.js';`
> Note: you can give the default import any name you want. Not for named import though

`Named exports` have to be imported by their name:
`import { someData } from './path/to/file.js';`

You can import *all* `named exports` at once with the following syntax:
`import * as upToYou from './path/file.js';`

Access it is as simple as `upToYou.someData`.

## Classes

Classes are a feature which basically replace constructor functions and prototypes. You can define blueprints for JavaScript objects with them.

This is the old way:
```JS
    // ES6
    class Person {
        constructor() {
            this.name = 'Max';
        }
    }

    const person = new Person();
    console.log(person.name); // prints 'Max'
```

In modern JS projects, you can define class this way, and its related methods:

The second approach has the same advantage as all arrow functions have: The `this` keyword doesn't change its reference.

```JS
    // ES7
    class Person {
        name = 'Max';

        printMyName () {
            console.log(this.name);
        }

        anotherMethod = () => {

        }
    }

    const person = new Person();
    console.log(person.name); // prints 'Max'
    person.printMyName(); // same.
```

You can also use **inheritance** when using classes:

```JS
    class Human {
        species = 'human';
    }

    class Person extends Human {
        name = 'Max';
        printMyName = () => {
            console.log(this.name);
        }
    }
    const person = new Person();
    person.printMyName();
    console.log(person.species); // print 'human'
```

## Spread & Rest Operator
The spread and rest operators actually use the same syntax: `...`

The spread operator allows you to pull elements out of an array (=> split the array into a list of its elements) or pull the properties out of an object. Here are two examples:
```JS
    constoldArray=[1,2,3];
    constnewArray=[...oldArray,4,5]; //Thisnowis[1,2,3, 4, 5];
```

Same goes to object.

The spread operator is extremely useful for cloning arrays and objects. Since both are reference types (and not primitives), copying them safely (i.e. preventing future mutation of the copied original) can be tricky. With the spread operator you have an easy way of creating a (shallow!) clone of the object or array.

For **restr** operator: it's used to merge a list of function arguments into an array. 
```JS
    function sortArgs (...args) {
        return args.sort()
    }
```
## Destructuring
Destructuring allows you to easily access the values of arrays or objects and assign them to variables.


# Create React App

```shell
    npx create-react-app react-complete-guide
    npm start // to start the application
```

## How to compose the applications. 
It's highly individualized. But there are some guidelines. 

- Keep App.js clean, mostly just for routing. 
- Keep a **component** folder. 
  - UI
  - Layout
  - Other categories of components. 

> While components are in this structure, it doesn't mean that css need to be re-written. Simply do the proper imports, the magic will happen.  One example:

```js
    // File: ./components/UI/Card
    // Notice how style is constructed dyanmically
    // and how props.children is passed down to Card.
    function Card(props) {
        const classes = 'card ' + props.className;
        return (
            <div className={classes}>
                {props.children}
            </div>
        )
    }

    ...

    ...
    // Another file in Expenses folder.
    // File: ./component/Expenses/ExpenseItem
    import Card from '../UI/Card';
    function ExpenseItem({date, title, amount}) {
        return (
            <Card className="expense-item">
                <ExpenseDate date={date}/>
                <div className="expense-item__description">
                    <h2>{title}</h2>
                    <div className="expense-item__price">
                        ${amount}
                    </div>
                </div>
            </Card>
   ) 
}

```

# State

Whenever updating a state that relies on previous state, make sure to use this format:
```js
setTitleState((prevState) => {
    return {
        ...prevState,
        newItem: 'newVal'
    }
})

```


## How to communicate from child to parent?
**Lifting State Up**
Basically, passing handler function from parent to children, then use `prop.definedEventHandler(updatedDataObject)` to pass the object back to parent. 


# React Modal via React Portal

Steps:
- Add modal to `public/index.html`, close to `#root` element
```js
<div id="overlays"></div>
```
- Create Modal
  A few notes:
  - use ReactDom
  - portalElement takes in both backdrop and modaloverlay
  - how props.children is used, to make the component generic
  
```js
import ReactDom from 'react-dom';

import classes from './Modal.module.css';

const Backdrop = (props) => {
  return <div className={classes.Backdrop}></div>;
};
const ModalOverlay = (props) => {
  return (
    <div className={classes.modal}>
      <div className={classes.content}>{props.children}</div>
    </div>
  );
};

const portalElement = document.getElementById('overlays');

const Modal = (props) => {
  return (
    <>
      {ReactDom.createPortal(<Backdrop />, portalElement)}
      {ReactDom.createPortal(<ModalOverlay>{props.children}</ModalOverlay>, portalElement)}
    </>
  );
};

export default Modal;

```
- import Modal in Cart


# Composition

The structure is organized like this:
- assets
- components
  - Layout
  - UI
  - [features: Cart, Meals...]
- store
  - cart-context.js
  - CartProvider.js

# Context

Usually add 'store' folder parallel to components, assets folder. 

## Create Context

Adding initial values helps with auto-completion in vscode.
```js
// cart-context.js
import { createContext } from 'react';

const CartContext = createContext({
  items: [],
  totalAmount: 0,
  addItem: (item) => {},
  removeItem: (id) => {},
});

export default CartContext;
```

## set Provider
```js
// CartProvider.js
import CartContext from './cart.context';

// the following are concrete values

const CartProvider = (props) => {
  const addItemHandler = (item) => {};

  const removeItemHandler = (id) => {};

  const cartContext = {
    items: [],
    totalAmount: 0,
    addItem: (item) => addItemHandler,
    removeItem: (id) => removeItemHandler,
  };
  return <CartContext.Provider value={cartContext}>{props.children}</CartContext.Provider>;
};

```

## Wrap the provider around where the context is used
```js
<CartProvider>
...
   <header>
   <Main>...</Main>
</CartProvider>
```

## Use the context
```js
  const cartCtx = useContext(CartContext);
  // .reduce reduces the array into a single value. a single number in this case.
  // It takes two arguments:
  // 1. function: also takes two arguments: curNumber, item
  // 2. start value
  const numberOfCartItems = cartCtx.items.reduce((curNumber, item) => {
      return curNumber + item.amount
  }, 0);
  ...
  <div>
    {numberOfCartItems}
  </div>
```


## Modify context

```js
import { useReducer } from 'react';
import CartContext from './cart.context';

// setup default state
const defaultCartState = {
  items: [],
  totalAmount: 0,
};
// reducer can be outside, 
const cartReducer = (state, action) => {
  return defaultCartState;
};

const CartProvider = (props) => {
  // useReducer takes two element: reducer function and default state. 
  // then returns two elements: current state, and dispatch function.
  const [cartState, dispatchCartAction] = useReducer(cartReducer, defaultCartState);
  const addItemHandler = (item) => {
    dispatchCartAction({ type: 'ADD', item: item });
  };

  const removeItemHandler = (id) => {};

  const cartContext = {
    items: cartState.items,
    totalAmount: cartState.totalAmount,
    addItem: (item) => addItemHandler,
    removeItem: (id) => removeItemHandler,
  };
  return <CartContext.Provider value={cartContext}>{props.children}</CartContext.Provider>;
};

export default CartProvider;


```

** create new array to existing ones *** 
```js
const updatedItems = state.items.concat(item)
```

## Wire up context with useState to update Context

```js
import { useReducer } from 'react';
import CartContext from './cart.context';

const defaultCartState = {
  items: [],
  totalAmount: 0,
};
const cartReducer = (state, action) => {
  if (action.type === 'ADD') {
    const updatedItems = state.items.concat(action.item);
    const updatedTotalAmount = state.totalAmount + action.item.price * action.item.amount;
    return { items: updatedItems, totalAmount: updatedTotalAmount };
  }
  return defaultCartState;
};

const CartProvider = (props) => {
  const [cartState, dispatchCartAction] = useReducer(cartReducer, defaultCartState);
  const addItemHandler = (item) => {
    dispatchCartAction({ type: 'ADD', item: item });
  };

  const removeItemHandler = (id) => {
    dispatchCartAction({ type: 'REMOVE', id: id });
  };

  const cartContext = {
    items: cartState.items,
    totalAmount: cartState.totalAmount,
    addItem: (item) => addItemHandler,
    removeItem: (id) => removeItemHandler,
  };
  return <CartContext.Provider value={cartContext}>{props.children}</CartContext.Provider>;
};

export default CartProvider;

```


## How to ForwardRef to element

If a customized element has 'ref' required, here is how to use `forwardRef` from React to get it working. It takes two arguments, the normal `props` and `ref`.  Then the customized <Input> can use `ref`
```js
import { forwardRef } from 'react';
import classes from './Input.module.css';

const Input = forwardRef((props, ref) => {
  return (
    <div className={classes.input}>
      <label htmlFor={props.input.id}>{props.label}</label>
      <input ref={ref} {...props.input} />
    </div>
  );
});

export default Input;


```


# useMemo and useCallback

- useMemo wrap around a component and will not re-run if atributes are not changed. One gotcha is that functions won't be counted since they are not primitive types, similary to array, object, etc. 
- useCallback wraps around a function and re-use that function. It solves the problem above with useMemo



# async/await

async/await is not React specific.  Here is a conversion between fetch.then.catch and async/await+try+catch (response has 'ok' field, which tells whether request is successful or not. it also has a 'status' field, which we can manually check which status it is.)

```
fetch(`url`)
.then(response => response.json())
.then(response => ...)
.catch(err => ...)
```

```
async function () => {
  try {
    const response = await fetch(`url`);
    // Notice how `response.ok` is used here to catch errors.
    if (!response.ok) {
      throw new Error('Something is wrong here')
    }
    const data = await response.json()
  } catch (err) {
    ...
    setError(err.message)
  }
}

# Custom Hooks

- Create 'hooks' folder, parallel to 'components' folder.
- name it something like 'use-http.js', 'use-counter.js'. 
- Inside the file, it has to be a function start with 'use' to signal to React that it's a custom hook.

```JS
// use-counter.js

import { useState, useEffect } from 'react';

const useCounter = () => {
  const [counter, setCounter] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setCounter((prevCounter) => prevCounter + 1);
    }, 1000);

    return () => clearInterval(interval);
  }, []);

  // return counter, no need to return setCounter? 
  return counter;
};

export default useCounter;

```

use-http.js hook

```
import { useState } from 'react';

const useHttp = (requestConfig, applyData) => {
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);

  const sendRequest = async (taskText) => {
    setIsLoading(true);
    setError(null);
    try {
      const response = await fetch(requestConfig.url, {
        method: requestConfig.method,
        headers: requestConfig.headers,
        body: JSON.stringify(requestConfig.body),
      });

      if (!response.ok) {
        throw new Error('Request failed!');
      }

      const data = await response.json();
      applyData(data);
    } catch (err) {
      setError(err.message || 'Something went wrong!');
    }
    setIsLoading(false);
  };

  return {
    isLoading,
    error,
    sendRequest,
  };
};

export default useHttp;

```


Make something an alias, use ':'

Example:
```
  const {
    isLoading,
    error,
    // notice here for alias
    sendRequest: fetchTasks,
  } = useHttp(
    {
      url: 'https://ffistertwitbot-default-rtdb.firebaseio.com/test.json',
    },
    transformTasks
  );

```

Figure out how javascript `bind` work

```
const NewTask = (props) => {
  const createTask = (taskText, data) => {
    const generatedId = data.name; // firebase-specific => "name" contains generated id
    const createdTask = { id: generatedId, text: taskText };

    props.onAddTask(createdTask);
  };
  const { isLoading, error, sendRequest: saveTask } = useHttp();
  const enterTaskHandler = (taskText) => {
    saveTask(
      {
        url: 'https://ffistertwitbot-default-rtdb.firebaseio.com/test.json',
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: { text: taskText },
      },
      // notice here:
      // .bind: first paramter is 'this', it can be ignored here. 
      // second one is a new variable. 
      // then from the rest on is the original default parameters passed in original function.
      // This is very flexible. so cool!
      createTask.bind(null, taskText);
    );
  };

  return (
    <Section>
      <TaskForm onEnterTask={enterTaskHandler} loading={isLoading} />
      {error && <p>{error}</p>}
    </Section>
  );
};
```


# 16 Forms

# 20 Routing

## Install
Pay attention it's router-dom, not router. 
`npm install react-router-dom`.