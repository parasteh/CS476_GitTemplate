# Introduction & Getting Started with Vue.js Version 3

Vue.js is an open-source JavaScript framework for building user interfaces and single-page applications. It was created by Evan You in 2014 and has gained a lot of popularity in recent years due to its simplicity and flexibility.

One of the key features of Vue.js is its reactive data binding system, which allows developers to build complex UIs with ease. This means that any changes made to the data in the application automatically update the corresponding UI components. Vue.js also offers a virtual DOM (Document Object Model) which enhances performance by minimizing DOM updates.

In this guide, we'll go through the basics of Vue.js and learn how to build a simple Vue.js application.

## Prerequisites

Before you begin, you'll need to have the NPM installed:

[NPM](https://nodejs.org/en/) (version 16 or higher)

## Installation

To get started with Vue.js 3, you can either use the Vue CLI or include Vue.js in your HTML file using a CDN.

### Step 1: Create new Vue 3 project using Vue CLI

Vue CLI is a command-line interface for quickly scaffolding Vue.js projects. To install [Vue CLI](https://cli.vuejs.org/), open a terminal window and run the following command:
```bash
npm install -g @vue/cli
vue create my-project
```

This will create a new Vue.js project in a directory called `my-project`.

### Step 2: Build a simple component

Now that we have a new Vue 3 project, let's create a simple component. Create a new file called HelloWorld.vue in the `src/components` directory with the following content:

```html
<template>
  <div>
    <h1>Hello World!</h1>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld'
}
</script>
```

### Step 3: Use the component in App.vue

Now that we have a new component, let's use it in App.vue. Replace the contents of App.vue with the following code:

```html
<template>
  <div id="app">
    <HelloWorld />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

```

### Step 4: Run the App

We're now ready to run the app. In the project directory, run:

```bash
npm run serve
```
### Other option is using Vue from CDN

If you don't want to use Vue CLI, you can also use Vue directly from a CDN via a script tag: 

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

```

When using Vue from a CDN, there is no "build step" involved. This makes the setup a lot simpler, and is suitable for enhancing static HTML or integrating with a backend framework. However, you won't be able to use the Single-File Component (SFC) syntax.

## Popular Vue 3 frameworks that you might find useful

- [Vite:](https://vitejs.dev/) a fast and lightweight development server and build tool for modern web development.
- [Nuxt.js:](https://nuxtjs.org/) a progressive framework based on Vue.js to create modern web applications. It provides server-side rendering and other powerful features out of the box.
- [Quasar:](https://quasar.dev/) a full-stack framework for building high-performance and responsive web applications. It comes with a rich set of pre-built components and plugins.
- [VuePress:](https://vuepress.vuejs.org/) a static site generator based on Vue.js, which is ideal for creating documentation sites and blogs.
- [Element Plus:](https://element-plus.org/en-US/) a UI library based on Vue.js 3 that provides a set of elegant and customizable components for building web applications.

There are many other Vue 3 frameworks and libraries available as well, so be sure to check out the official Vue.js website for more information: https://v3.vuejs.org/ecosystem/frameworks.html


*Good job! You've made it to the end of the Vue 3 guide. Hope you found this documentation helpful*
