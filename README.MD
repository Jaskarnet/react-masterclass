**Table of contents**

- [1. Setuping react project](#1-setuping-react-project)
- [2. JavaScript refresher](#2-javascript-refresher)
- [3. React Essentials](#3-react-essentials)
  - [3.1. Components](#31-components)
  - [3.2. index.jsx](#32-indexjsx)
  - [3.3. Built-in vs custom components](#33-built-in-vs-custom-components)
  - [3.4. Dynamic values inside JSX](#34-dynamic-values-inside-jsx)
  - [3.5. Loading images](#35-loading-images)


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

Instead you should use import with relative path to this file `import reactImg from './assets/image-name.png'`