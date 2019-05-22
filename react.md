# app-architecture

👨‍🏫 Explanation of modern web development and architectures. Sources are listed. Pull requests are welcome! 

## Table of Contents

* [GitHub](#github)
* [Dependent Services](#refrain-from-dependent-services)
* [Functional Services](#functional-services)
* [React](#react)
* [Code quality](#code-quality)
* [Testing and coverage](#testing-and-coverage)

## GitHub 👨‍💻

- Issues
- Pull Requests
  - Reviews
- Project Documentation and Scope

## Composition

## Refrain from Dependent Services 

Keeping services focused and performing a particular task enables us to not worry if another service is down. If another service fails, you can retry that specific step without having to reprocess the entire request again. Only the failed function will be performed.

## Functional Services ℷ

### Functional

`Functional programming` or `Declarative programming` is a programming paradigm :thinking:, with adjacent programming concepts being `Object-oriented programming` :dog: and `Imperative programming` :point_right:. Functional programming focuses on creating functions and declare that functions are King 🤴.  

__Declarative__ 👑 programming states that a task needs to happen without going into every detail of that `action`. This method is a form of [functional composition](https://en.wikipedia.org/wiki/Function_composition), in that different tasks are broken into smaller functions which call each other upon each step when eventually return to the original calling function. 

### Abstraction 🤩

*[Abstraction](https://developer.mozilla.org/en-US/docs/Glossary/Abstraction) in computer programming is a way to reduce complexity and allow efficient design and implementation in complex software systems. It hides the technical complexity of systems behind simpler APIs.* (Source: [Mozilla](https://developer.mozilla.org/en-US/docs/Glossary/Abstraction))

[__Advantages of Data Abstraction__](https://developer.mozilla.org/en-US/docs/Glossary/Abstraction#Advantages_of_Data_Abstraction)
* Helps the user to avoid writing low level code.
* Avoids code duplication and increases reusability.
* Can change internal implementation of class independently without affecting the user.
* Helps to increase security of an application or program as only important details are provided to the user.


[Lambda calculus](https://crypto.stanford.edu/~blynn/lambda/) and [functional programming](https://opensource.com/article/17/6/functional-javascript) are the few main concepts in creating microservices architectures.
Functional programming follows a strict set of rules for dealing with data and manipulating replicated data instead of original data.

A __Component__ :cake: is a piece of software that follows the functional programming concept of [pure functions](https://en.wikipedia.org/wiki/Pure_function), :innocent: that is, given the same values as parameters of a function, that function will always return the same value, and avoids [side effects](https://en.wikipedia.org/wiki/Side_effect_(computer_science)). :sparkles:

A component can be the proocess for starting the app. Given the same application, host, and data, an application will always perform the starting steps, and will avoid side effects.

Side [effects](https://en.wikipedia.org/wiki/Side_effect_(computer_science)) are anything that are passed as a parameter to a function but that parameter does not always have an immutible value. If you pass this as a parameter, this means the function is not `pure` :innocent: since the value of the parameter may be changing.

## React ⚛️

React is a view layer 👀, declarative library for creating user interfaces. React is currently maintained and released by Facebook.

In [react](https://reactjs.org/docs/components-and-props.html#function-and-class-components), components can be written as either a `class` or as a `function`. There are various advantages to either approach but ideally you want to have stateless `function` components. In the past, react only allowed `class` components to manage/display state of your app but this is no longer the case. With the addition of [Hooks](https://reactjs.org/docs/hooks-intro.html) 🎣, you can add state to your functional components and refrain from adding `lifecycle methods` like `componentDidMount, componentWillMount, and componentWillUnmount` to manage state. Just `import React, { useState } from 'react';` in the top line of your react component (in react version 16.8.\*) to add state to your function components. 

Declaring functional components is not the same. Using a variable declaration and setting that to an `arrow function` ➡️ or function expression is not the same as using `function expression` alone. For example:

```js
// Figure A.
let NewComponent = (props) => (
  <div>{props.title}</div>
);
```

should not be confused and treated the same as:

```js
// Figure B.
function NewComponent(props) {
  return <div>{props.title}</div>
}
```

The way JavaScript works when the code is compiled and ran, is that __all__ variables are hoisted ⤴️ to the top of the current scope. Therefore, `let NewComponent` line will be first undefined until later in the program when NewComponent is assigned to a function. Below is an example of when a program is compiled after being transpiled from [__Babeljs__](https://babeljs.io/).

```js
// Figure C.

// Global scope
var NewComponent; // undefined

...

var NewComponent = function(props) { // NewComponent is then defined later as a function
  return <div>{props.title}</div>;
}
```

For more information on scope, [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Scope) has some great documentation on how JavaScript treats variables in their own scope. 🔭

In summary, if you are writing top-level components, follow the `function expression` method.

### JSX

In react, there are plugins added to Babel which allow you to write HTML code inside of a JavaScript function. Without this plugin, you would have to manually write HTML in JavaScript. For example:

```js
// Figure D.

function NewComponent(props) {
  return (
    <div>
      <img src="avatar.png" class="profile" />
      <h3>{`${props.firstName} ${props.lastName}`}</h3>
    </div>;
  );
}

// Compiles to...

var NewComponent = React.DOM.div(props,
  React.DOM.img({ src: "avatar.png", "class": "profile" }),
  React.DOM.h3(props, [props.firstName, props.lastName].join(" "))
);
```

Babel plugins [abstract](#abstraction) away this complexity and allow you to move forward with creating views in react.

### Component Design: `function` expression or `class` expression

In React, you can develop components in one of two ways: a `function() {}`, or `class Component extends React.Component`. :sparkles: 
There are advantages to using one before the other, and this section looks to define why you should write `function` components. 👩‍🎤

When React released version `16.8.0` the React core team released the newest feature called __Hooks__. With hooks, you can write function expression components and also apply `state`! Before, you only wrote `function` components when you wanted to write components that were `pure`, with this new Hooks addition you can finally add `state` and effects to your `function` components by importing the new modules into your component: `import React, { useState, useEffect, } from 'react'`.

You may still use `class` components, but it is important to know the motivation behind adding Hooks to React. [Read more at reactjs.org](https://reactjs.org/docs/hooks-intro.html#motivation).

*What if I want to keep using class components?*
Best practices in writing `class` components have also changed. 👩‍🏫 To see how your classes should be changed, please continue reading below! 👇

[Update on async rendering - reactjs.org Blog](https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html#initializing-state)

### State 😍😠🙂😭😬

State can be managed in either `class` components or `function` components since [__react version 16.8__](https://reactjs.org/docs/hooks-intro.html). However, as your app grows the incoming problem that arises is managing state across a large component tree. React encourages that you __hoist__ state to the topmost, common component and pass state as a prop to lower level components.

This is helpful in its own scope but may not fix every issue when managing scope. 

* What if you wanted application-level scope in your app? 
* What if all state is eventually added to the topmost component?

This is where [Redux](https://redux.js.org/faq/react-redux#redux-faq-react-redux) ⚛️ becomes useful. Redux allows you to manage your state on the application level and [abstract](#abstraction) away the complexity of managing your state.

## Code quality 🛁🤷‍♂️💫

- ESlint (JavaScript-specific)
- Prettier

## Testing and Coverage 🚧🏗👷‍♀️👷‍♂️

- [Jest](https://jestjs.io/) (Facebook)
- [Enzyme](https://airbnb.io/enzyme/) (Airbnb)

Writing component tests assure that the component will work in a variety of scenarios. Tests also assure that you are cleaning up the component and are writing the appropriate `lifecycle methods` on your `class` components.

When writing your components, it is important to keep it as small as possible in favor of component [composition](#composition). Not only composition is the reason for small components, but another reason may be for writing tests! A small component may have to go through a large amount of cases in order to define if it is working properly when it is __stateless__, and __stateful__ components will have to go through even more cases to determine its predicted outcome. 

Keeping your components small will help in the testing process. You'll thank yourself later. 
