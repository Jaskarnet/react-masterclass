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
  image={componentsImg}
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
React by default ignores in put between opening and closing component tags. To use something like `<TabButton>Components</TabButton>` you need to add parameter (usually called props) to a component function signature as usual. There is a special built-in children prop (`props.children`). This children prop simply refers to the content between component tags.

## 3.9. Reacting to events
In vanilla JS to react to event for a button click you would do something like this `document.querySelector('button').addEventListener('click', () => {})`.

In a React project we don't want to write imperative code like this, instead we want to write declarative code. You can do that by adding special attribute (special prop) to elements.

There are many special props which name starts with `on`. Their value is always a funcion.

The function name convention for special prop is to use *handle* + *name of the event* (e.g.: `handleClick`). Another common option is to call it *name of the event* + *Handler* (e.g.: `clickHandler`)

### 3.9.1. `onClick` prop
```jsx
export default function TabButton({children}) {
    function handleClick() {
        console.log('Hello World!');
    }

    return <li><button onClick={handleClick}>{children}</button></li>
}
```

