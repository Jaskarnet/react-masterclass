**Table of contents**

- [1. Setuping react project](#1-setuping-react-project)
- [2. JavaScript refresher](#2-javascript-refresher)


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

