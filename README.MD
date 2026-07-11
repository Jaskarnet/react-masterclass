**Table of contents**

- [1. Setuping react project](#1-setuping-react-project)
- [2. JavaScript refresher](#2-javascript-refresher)
- [3. React Essentials](#3-react-essentials)
  - [3.1. Components](#31-components)
  - [3.2. index.jsx](#32-indexjsx)
  - [3.3. Built-in vs custom components](#33-built-in-vs-custom-components)
  - [3.4. Dynamic values inside JSX](#34-dynamic-values-inside-jsx)
  - [3.5. Loading images](#35-loading-images)
  - [3.6. Props](#36-props)
  - [3.7. Project Structure](#37-project-structure)
  - [3.8. Component composition - special `children` prop](#38-component-composition---special-children-prop)
  - [3.9. Reacting to events](#39-reacting-to-events)
    - [3.9.1. `onClick` prop](#391-onclick-prop)
  - [3.10. State](#310-state)
  - [3.11. Rendering output conditionally](#311-rendering-output-conditionally)
    - [3.11.1. Using the ternary operator](#3111-using-the-ternary-operator)
    - [3.11.2. Using logical AND (`&&`)](#3112-using-logical-and-)
    - [3.11.3. Using variables](#3113-using-variables)
  - [3.12. CSS styling and dynamic styling](#312-css-styling-and-dynamic-styling)
  - [3.13. Outputting list data automatically](#313-outputting-list-data-automatically)
- [4. React Essentials - Deep Dive](#4-react-essentials---deep-dive)
  - [4.1. You don't have to use JSX](#41-you-dont-have-to-use-jsx)
  - [4.2. Working with Fragments](#42-working-with-fragments)
  - [4.3. When should you split components?](#43-when-should-you-split-components)
  - [4.4. Props are not forwarded automatically](#44-props-are-not-forwarded-automatically)
  - [4.5. Multiple JSX slots](#45-multiple-jsx-slots)
  - [4.6. Setting component types dynamically](#46-setting-component-types-dynamically)
  - [4.7. Setting default prop values](#47-setting-default-prop-values)
  - [4.8. Not all content must go into components](#48-not-all-content-must-go-into-components)
  - [4.9. Public folder](#49-public-folder)
  - [4.10. When to create a component](#410-when-to-create-a-component)
  - [4.11. Updating state based on previous state](#411-updating-state-based-on-previous-state)
    - [4.11.1. Why do you pass a function?](#4111-why-do-you-pass-a-function)
  - [4.12. Update object-state immutably](#412-update-object-state-immutably)
  - [4.13. Lifting the state up](#413-lifting-the-state-up)
- [5. React behind the scenes - optimization techniques](#5-react-behind-the-scenes---optimization-techniques)
  - [5.1. How does React update the DOM?](#51-how-does-react-update-the-dom)
  - [5.2. Optimization](#52-optimization)
    - [5.2.1. `React.memo()`](#521-reactmemo)
    - [5.2.2. Avoid component function executions with clever structuring](#522-avoid-component-function-executions-with-clever-structuring)
    - [5.2.3. `useCallback()` hook](#523-usecallback-hook)
    - [5.2.4. `React.useMemo()`](#524-reactusememo)

# 1. Setuping react project

1. Special project setup is needed for react app as we'll be using html in javascript (jsx) ![html-in-javascript](images/image.png) and it does not work in the browser ![react-code-to-browser](images/image-1.png)
2. One option without installing anything is to use webapp by typing `react.new` in browser
3. for local in IDE Vite (pronounced "wit") or create-react-app is needed
4. those tools use node.js so you need to install it
5. steps for creating project in Vite:
   1. type `npm create vite@latest <project_name>`
   2. select a framework - React
   3. select a variant - TypeScript
   4. `npm install`
   5. `npm run dev` - starts a development preview server that allows you to view the web app you're working on (quit it anytime using ctrl+c)

# 2. JavaScript refresher

Normal html with js projects need script tags in html file. In React you will not link them manually as **React projects use a build process**. This means that the code you write is not the code that gets executed (like this) in the browser.
It's React-scripts package (can be seen in package.json) that takes your code and transform it behind the scenes. It one of things is injecting sript tags to html file.
![alt text](images/image-2.png)

In React during import statements you omit extension of a file (as opposed in raw js where typically '.js' should be added to file name).

To use import and export in js file you would need to add attribute 'type="module"' to script tag in html file, but react's auto-injected script tags do not have them. That's because build process will merge those seperate files you have during development into one big file (or a bunch of big files) imported with old-school syntax in the right order. This is made to make this code execute in browsers that do not support this import-export syntax.

# 3. React Essentials

## 3.1. Components

Reusable building blocks.

![creating-components](images/image-3.png)
![why-components](images/image-4.png)
![jsx](images/image-5.png)

Component is a really just a JavaScript function. But to be recognised as a component by a React it must follow two rules:

1. Name starts with uppercase character
2. It returns a "Renderable" content

![component-signature-rules](images/image-6.png)

In JS u would use a function `function Header() {}` by executing it `Header()` but that's not how you use components in React. You can use your function as regular HTML element inside JSX code `<Header></Header>`. You could also use self-closing syntax `<Header />`.

## 3.2. index.jsx

_index.jsx_ file acts as a main entry point of React App since it is the first file to be loaded by the HTML file. ReactDOM library (which we import in this file) renders this app component. It is responsible of putting App component contents on the screen. It is rendered by passing jsx code to the `render` method. This `render` method is called on a object that's created by another method (`createRoot` method). `createRoot` method takes existing HTML element as an input (so an element that's not being created by a React, but rather is in _index.html_ file already). So `render` method takes component and renders it inside HTML element.
![index.jsx](images/image-7.png)
![root-component](images/image-8.png)
![component-hierarchy](images/image-9.png)

## 3.3. Built-in vs custom components

![built-in-vs-custom-components](images/image-10.png)

## 3.4. Dynamic values inside JSX

To place a dynamic value in JSX you need to use curly braces `{}`.

## 3.5. Loading images

You shouldnt use standard `<img src="path/to/image" alt="image description" />`.

Instead you should use import with relative path to this file `import reactImg from './assets/image-name.png'` and then inside JSX `<img src={reactImg} alt="Image description" />`.

## 3.6. Props

React allows you to pass data to components. via a concept called **props**.
The parameters in function signature of components are what in React is called props. They are called with the value taken from JSX tag attributes, fe:

```html
<CoreConcept
  title="Components"
  description="The core UI building block."
  image="{componentsImg}"
/>
```

```JSX
function CoreConcept(props) {
  return (
    <li>
      <img src={props.image} alt="">
        <h3>props.title</h3>
        <p>props.description</p>
      </img>
    </li>
  );
}
```

## 3.7. Project Structure

Best practice is to store one component per file. Those files are usually stored in a _components_ subfolder of _src_ folder. The convention is to name those files the same name as the component name that will be stored in that file. Most of the time exporting is done using `default` keyword.

Css files related to components should have the same name as the component file and put in the same folder. They are then imported in a related component file.

Be careful as those styles in css file are **NOT** scoped only to this component. Splitting the css code into the component specific css files can still make sense since it makes it easy to see which style SHOULD relate to which component, making adjusting those styles easier.
(There is a solotion to this potential problem. Later in course.)

There is an option to create a folder for each group of files related to component, named the same as component file. This is not required and comes down to personal preference.

## 3.8. Component composition - special `children` prop

React by default ignores input between opening and closing component tags. To use something like `<TabButton>Components</TabButton>` you need to add parameter (usually called props) to a component function signature as usual. There is a special built-in children prop (`props.children`). This children prop simply refers to the content between component tags.

## 3.9. Reacting to events

In vanilla JS to react to event for a button click you would do something like this `document.querySelector('button').addEventListener('click', () => {})`.

In a React project we don't want to write imperative code like this, instead we want to write declarative code. You can do that by adding special attribute (special prop) to elements.

There are many special props which name starts with `on`. Their value is always a funcion.

The function name convention for special prop is to use _handle_ + _name of the event_ (e.g.: `handleClick`). Another common option is to call it _name of the event_ + _Handler_ (e.g.: `clickHandler`)

### 3.9.1. `onClick` prop

```jsx
export default function TabButton({ children }) {
  function handleClick() {
    console.log("Hello World!");
  }

  return (
    <li>
      <button onClick={handleClick}>{children}</button>
    </li>
  );
}
```

## 3.10. State

By default React component funtions execute only once. So if there is a change in displayed content there is a way to tell react to execute component function again.

State is all about registering variables that are handled by React and are updated with the help of a function that's provided by React, that will also tell React that data changed, that will therefore cause React to update the UI.

Those special variables are created with the help of the special function that must be imported from React library.

```jsx
import { useState } from "react";
```

This are so called React hook. All these funtions that start with 'use' in React projectsare React hooks. Special thing about React hooks is that they are technically regular functions, but they must ONLY be called inside of React component functions, or inside of other React hooks (e.g. custom React hooks).

You must call those hook functions directly inside of the component functions, not nested inside some other code (e.g. not nested inside of inner function of component function). It must be called on the top level of component function.

![react-hooks](images/image-11.png)

`useState` is one of the most important hooks offered by React, because that's the hook that will allow us to manage component specific state, which is simply some data stored by React, which when changed will trigger this component function, to which this hook belongs, to re-execute.

`useState` accept an argument which is default value React will store and use the first time component is rendered. `useState` also returns a value which can be stored in variable or constant (it doesnt matter). This value is an array which has exactly 2 elements. Commonly it is received using array destructuring to store these 2 elements in 2 seperate constants. Common naming convention is to use something like:

```jsx
const [selectedTopic, setSelectedTopic] = useState("Please click a button");
```

First element in returned array from setState is the current data snapshot for this component execution cycle. So for first execution of component function it will be this initial value. If it's executed again for some reason it will be the updated value.

The second element will always be a function. A function provided by React that can be executed to update this state (this stored value). ut in addition to updating this stored value, calling this special function will also tell React that component function must be executed again.

We can use const here because value stored as state will be recreated everytime this component function executes. But behind the scenes React will update the actual value that will be passed on to this constant when this component function executes again.

![alt text](images/image-12.png)

**Two rules of hooks**:

- only call hooks at the top level
- only call hooks from react funtions (component functions or custom hooks)

**Derived state**:

- If you can calculate something from existing data during render, you should NOT put it in state.

## 3.11. Rendering output conditionally

### 3.11.1. Using the ternary operator

You can putt null in JSX code then nothing will be rendered. Useful in ternary operators inside JSX code.

```jsx
{
  !selectedTopic ? <p>Please select a topic.</p> : null;
}
```

### 3.11.2. Using logical AND (`&&`)

or using `&&`

```jsx
{
  !selectedTopic && <p>Please select a topic.</p>;
}
```

### 3.11.3. Using variables

or store it in variable

```jsx
// inside component function
let tabContent = <p>Please select a topic.</p>;

if (selectedTopic) {
  tabContent = (
    <div id="tab-content">
      <h3>{EXAMPLES[selectedTopic].title}</h3>
      <p>{EXAMPLES[selectedTopic].description}</p>
      <pre>
        <code>{EXAMPLES[selectedTopic].code}</code>
      </pre>
    </div>
  );
}

return { tabContent };
```

## 3.12. CSS styling and dynamic styling

In standard html to change declare class you would use `class` prop. But there is React specific built-in prop `className`. Most of other attributes like `id` and so on are the same in JSX and HTML. Just for this class attribute it's different.

## 3.13. Outputting list data automatically

As React can output array of JSX elements but not array of js objects, we need to transform them to JSX elements. We can achieve that by using `Arrays.map()` method.

```jsx
// inside renderable content
{
  CORE_CONCEPTS.map((conceptItem) => (
    <CoreConcept {...conceptItem} key={conceptItem.title} />
  ));
}
```

When dynamically outputting a list of elements, every element should receive a unique "key" to help React tell the list items apart.

# 4. React Essentials - Deep Dive

## 4.1. You don't have to use JSX

As a React developer you should know that in theory you could build React apps without using JSX and therefore without need of special build process. Vast majority of React projects use JSX though.

![you-don't-need-jsx](images/image-13.png)

## 4.2. Working with Fragments

JSX expressions must have one parent element. That's because in the end JSX is syntactic sugar over `React.createElement` function which expects one argument. That's why there's often a need to wrap sibling elements in opening and closig div tags. This limitation means that you do end up with empty div in your DOM structure.

That's why there's an alternative. There is a wrapper if u do need a root component to wrap some sibling components, but you dont want to render an actual element to the screen. For this you can import Fragment component like this:

```jsx
import { Fragment } from "react";
```

and use it instead of div as a wrapper for renderable content.

Modern React projects use even shorter alternative. There you don't even need to import Fragment. You just use empty tags as a wrapper, so end code would look like this:

```jsx
return {
  <>
    <Header />
    <main>
    </main>
  </>
}
```

## 4.3. When should you split components?

Put different features into different components.
If you managing the state of the inner component, then you probabli want to split up.

## 4.4. Props are not forwarded automatically

![props-are-not-forwarded-automatically](images/image-14.png)

To solve this problem we could in component function accept all of the needed attributes and forward them manually. That can cause a lot of manual work and isn't really scalable.

We can use a pattern called **Forwarded Props** or **Proxy Props**.

It is used using standard JS **rest property** (`...`) at the end of component function parameters declaration. This syntax group all remaining object properties into a new object. It is usually named _props_.

It is a usefull pattern when building wrapper components.

## 4.5. Multiple JSX slots

As we know we can use special `children` prop to access JSX within opening and closing tag of our component. But it isn't the only place where JSX code is accepted. Actually any prop can take JSX code so we can use it in dumb component to enforce some kind of structure without being overly specific:

```jsx
export default function Tabs({ children, buttons }) {
  return (
    <>
      <menu>{buttons}</menu>
      {children}
    </>
  );
}
```

## 4.6. Setting component types dynamically

You can make a prop that will represent the type of inner component in your returned renderable content. This prop takes component identifier. Custom components must be passed as a dynamic value (enclosed with `{}`, e.g.: `{Section}`) and built-in components must be passed as a string (enclosed with `""`, e.g.: `"menu"`).

Component with dynamic inner component types would look like this:

```jsx
export default function Tabs({ children, buttons, buttonsContainer }) {
  const ButtonsContainer = buttonsContainer;
  return (
    <>
      <ButtonsContainer>{buttons}</ButtonsContainer>
      {children}
    </>
  );
}
```

Important thing there is that we can't use `buttonsContainer` prop directly as a tag name as it starts with lowercase letter, and that would mean in JSX to look for a built-in componenent `buttonsContainer` which doesnt't exists. Thus we create const with name starting with uppercase letter and use it in a tag instead. We could of course take a shortcut and just name this prop with leading uppercase character.

Then we would use it like this with custom component:

```jsx
<Tabs buttonsContainer={Section}></Tabs>
```

or like that with built-in component:

```jsx
<Tabs buttonsContainer="menu"></Tabs>
```

## 4.7. Setting default prop values

Just like in JS.

ButtonsContainer example:

```jsx
export default function Tabs({ children, buttons, ButtonsContainer = "menu" }) {
  return (
    <>
      <ButtonsContainer>{buttons}</ButtonsContainer>
      {children}
    </>
  );
}
```

## 4.8. Not all content must go into components

While working in React it is easy to forget that content that displays static data (e.g.: header with a picture) that does not rely on props does not have to be a component. We can just use standard html in index.html.

## 4.9. Public folder

The public/ Folder
As shown in the previous lecture you can store images in the public/ folder and then directly reference them from inside your index.html or index.css files.

The reason for that is that images (or, in general: files) stored in public/ are made publicly available by the underlying project development server & build process. Just like index.html, those files can directly be visited from inside the browser and can therefore also be requested by other files.

If you try loading localhost:5173/some-image.jpg, you'll be able to see that image (if it exists in the public/ folder, of course).

The src/assets/ Folder
You can also store images in the src/assets/ folder (or, actually, anywhere in the src folder).

So what's the difference compared to public/?

Any files (of any format) stored in src (or subfolders like src/assets/) are not made available to the public. They can't be accessed by website visitors. If you try loading localhost:5173/src/assets/some-image.jpg, you'll get an error.

Instead, files stored in src/ (and subfolders) can be used in your code files. Images imported into code files are then picked up by the underlying build process, potentially optimized, and kind of "injected" into the public/ folder right before serving the website. Links to those images are automatically generated and used in the places where you referenced the imported images.

Which Folder Should You Use?
You should use the public/ folder for any images that should not be handled by the build process and that should be generally available. Good candidates are images used directly in the index.html file or favicons.

On the other hand, images that are used inside of components should typically be stored in the src/ folder (e.g., in src/assets/).

## 4.10. When to create a component

when you need to repeat yourself codewise.

## 4.11. Updating state based on previous state

You should **NOT** update state based on the previous value of that state like this:

```jsx
function handleEditClick() {
  setIsEditing(!isEditing);
}
```

Instead, you should pass a function to that state-updating function:

```jsx
function handleEditClick() {
  setIsEditing((editing) => !editing);
}
```

This is a strong recommendation by the React team and best practise in real world. It is something you should simply memorize.

![updating-state-based-on-old-state](images/image-15.png)

### 4.11.1. Why do you pass a function?

Because this function you pass will be called by React and it will automatcally get the current state value as an input.

The correct approach might look overly complex and seem to behave the same.

To understand this it is important to know that React behind the scenes in the end is scheduling those state updates you are triggering with those state updating functions, like `setIsEditing`. So this state update is **not performed instantly**, instead it is scheduled by React to be performed in the future. Now, the future will probably be in 1 or 2ms, but it's not instant.

![react-is-scheduling-state-updates](images/image-16.png)

Take this code snippet as an example:

```jsx
function handleEditClick() {
  setIsEditing(!isEditing);
  setIsEditing(!isEditing);
}
```

If you don't know about how React works you might not get the result you might expect. Because you might expect that the first `setIsEditing` call is setting `isEditing` to the opposite of it currently is, and since it is `false` by default this should set it to `true`. And since we do the same in the next line we might expect to set it back to false. So you might expect that nothing happens.

But thats not what's happening - we set the value twice to true.

That's why we should pass an updater function to `setIsEditing` instead of a value. React passes the current state as an argument to the updater function, allowing us to calculate the next state from the latest value.

So this snippet will give us the expected result:

```jsx
function handleEditClick() {
  // editing => false
  setIsEditing((editing) => !isEditing);
  // editing => true
  setIsEditing((editing) => !isEditing);
  // editing => false
}
```

## 4.12. Update object-state immutably

If your state is an object or array you update that state in immutable way. That means you simply create a copy of the old state and then change that copy instead of existing object or array.

The reason is that if your state is an object or array you're dealing with a reference value in JS, and therefore if you would be updating it like this:

```jsx
// wrong way of updating state that is an object or array
function handleSelectSquare(rowIndex, colIndex) {
  setGameBoard((prevGameBoard) => {
    prevGameBoard[rowIndex][colIndex] = "X";
    return prevGameBoard;
  });
}
```

you would be updating the old value in memory immediately, even before this scheduled state update was executed by React. This can lead to strange bugs and side effects if you have multiple places in your application that are scheduling state updates for the same state.

```jsx
// correct way of updating state that is an object or array
function handleSelectSquare(rowIndex, colIndex) {
  setGameBoard((prevGameBoard) => {
    const updatedBoard = [
      ...prevGameBoard.map((innerArray) => [...innerArray]),
    ];
    updatedBoard[rowIndex][colIndex] = "X";
    return updatedBoard;
  });
}
```

## 4.13. Lifting the state up

If multiple components need the same information, we need to manage the state in the closest ancestor component, that has access to both components that need that information. Ancestor component will give that information tomcomponents via props.

![lifting-state-up](images/image-17.png)

# 5. React behind the scenes - optimization techniques

## 5.1. How does React update the DOM?

It updates from top to bottom of the tree. The App component is usally the top component. If any custom component is in renderable JSX part of it then it will render (execute component function) of this component as well and so on.

## 5.2. Optimization

### 5.2.1. `React.memo()`

To prevent unnecessary renders triggered by a parent component you can use `memo` function. Just wrap your component function as argument to memo function imported from React. To work in all cases Sonar would advise that instead of exporting directly this memo it is better to store it as a const (preferably with the same name as the component) first and then export this const.

This `memo` function prevents triggering component function if props are the same. It does not care about internal state though and will not prevent rerendering if state changes (`useState`).

**Don't overuse `memo()`**.

It might be tempting to wrap all your component functions in memo. But you should **NOT** do that. Checking props with `memo()` costs performance. If you wrap it around all your components it will add a lot of unnecessary checks.

Instead, **use it as high up in the component tree as possible**. Blocking a component execution there also block all child component executions.

### 5.2.2. Avoid component function executions with clever structuring

State changes and reexecutions of child components do **NOT** trigger parent component executions. Knowing that, moving state as low in the tree as possible is preferred.

### 5.2.3. `useCallback()` hook

In general, `useCallback` is a wrapper around an existing function. It is primarily used together with `React.memo`.

A common example is when you pass an `onClick` handler from a parent component to a child component. Even if the function's code stays the same, a new function is created every time the parent component re-renders. Because of that, `React.memo` treats it as a different prop and re-renders the child component.

To avoid this, we can let React manage the function's lifecycle by wrapping it in `useCallback()`. The hook returns a memoized version of the function, and it is common to store it in a `const` with the same name as the original function.

`useCallback` takes two arguments:

1. The function to memoize.
2. An array of dependencies.

As long as none of the dependencies change, `useCallback` returns the same function instance on every render. This allows `React.memo` to see that the prop has not changed and avoid unnecessary re-renders.

### 5.2.4. `React.useMemo()`

Just as you want to prevent component functions with `memo`, you also may want to prevent execution of normal functions that are called inside component functions, unless their import changed. React gives us `useMemo` hook.

- `memo` - wrapped around component functions
- `useMemo` - wrapped around normal functions inside component funcitons

`useMemo` takes two arguments:

1. A function that returns the value you want to memoize.
2. An array of dependencies.

```jsx
const sortedUsers = useMemo(() => {
  return users.sort((a, b) => a.name.localeCompare(b.name));
}, [users]);
```

In the example above, the sorting operation will only run again when `users` changes. On every other render, React returns the previously computed value.

This can be useful when:

- Performing expensive calculations.
- Filtering or sorting large arrays.
- Creating derived data from props or state.
- Returning objects or arrays that are passed to memoized child components.

For example:

```jsx
const filteredUsers = useMemo(() => {
  return users.filter((user) => user.active);
}, [users]);
```

Without `useMemo`, the filter operation would run on every render, even if `users` had not changed.

However, `useMemo` should **NOT** be used everywhere. Memoization also has a cost because React needs to store the previous value and compare dependencies on every render. For cheap calculations, `useMemo` can actually make your code more complicated without providing any performance benefit.
