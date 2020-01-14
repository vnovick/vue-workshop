# vue-workshop

# Day 1

- [Slides](https://slides.com/vladimirnovick/vue-workshop-day1?token=60MFptC4) Password `Playtech`
- [Codesandbox ToDo app](https://codesandbox.io/s/intro1-hqlfe)

### Excercise 1 

-----------------Ex1 - Basics ----------------------

- Start by including a script on the page [](https://unpkg.com/vue@2.6.11/dist/vue.js)
- install [Vue Devtools](https://github.com/vuejs/vue-devtools)
- click on a top right icon in Browser panel to open example app in a new window. Then Vue extension should detect Vue on the page. If it's not, you can check "Allow access urls" options in Chrome management panel (chrome://extensions)

- create new Vue instance to switch existing html to Vue
  present same data hardcoded in html in Vue by coppying html and using template prop of Vue instance(progressive enhancement)
- move a list of todos into data on Vue instance
- present a list of todos using v-for
- connect todo input field to Vue instance using v-model
- push and pop items from the array using Vue instance from Vue Devtools

----------------Ex2 - Events & methods ---------------------------

add submit method to add a new todo
try it out in Vue Devtools
connect todo input field to enter keycode for submitting todo
create removeTodo method and connect it to destroy button
add completed class
when double clicking on todo it should switch it to input field to update. For that change class to 'editing' and conditionally display input field.
update should be submitted when hitting Enter

--------------Ex3 - computed ----------------------

- connect "items left" field to Vue instance to display relevant data
- when clicking on completed todo checkbox - todo should be toggled as completed

-------------- Bonus --------------

Implement All, Active and Completed filters
clicking on filters should display either all items, completed or active.
disable submit button whenever there is no todo item
add 'enter' submittion rule
switch completed todo to strikethrough


[Excercise1 Solved](https://codesandbox.io/s/excercise1-b4kuf)

### Excercise 2 

1. create a new folder for your project
`npm init` 
`yarn add --dev webpack webpack-cli vue`

2. create folder structure

- /src 
- - /components 
- - /pages
- - index.js 
- - App.vue

3. add the following code to index.js
```
import Vue from 'vue'
import App from './App.vue'
new Vue({
  el: '#app',
  render: h => h(App)
})
```

4. create really basic App.vue template

```
<template>
  <div>
    <h1>Hello World!</h1>
  </div>
</template>

```

5. create webpack.config.dev.js to root folder
```
'use strict'
const { VueLoaderPlugin } = require('vue-loader')
module.exports = {
  mode: 'development',
  module: {
    rules: [
      {
        test: /\.vue$/,
        use: 'vue-loader'
      },
      {
        test: /\.css$/,
        use: [
          'vue-style-loader',
          'css-loader'
        ]
      }
    ]
  },
  plugins: [
    new VueLoaderPlugin()
  ]
}
```
6. install style and css loaders
`yarn add --dev vue-loader vue-template-compiler vue-style-loader css-loader`

7. add build script to package.json
`"build": "webpack --config build/webpack.config.dev.js"`

8. add `index.html` file from previous project

9. add `<script src="dist/main.js" type="text/javascript"></script>`

#### Add hot reload

- add dev server 

`yarn add --dev webpack-dev-server html-webpack-plugin`

- add dev script to `package.json`

`"dev": "webpack-dev-server --config webpack.config.dev.js"`

- add it to plugins array in `webpack.config.dev.js`

```
new webpack.HotModuleReplacementPlugin(),
new HtmlWebpackPlugin({
  filename: 'index.html',
  template: 'index.html',
  inject: true
})
```

- remove dist script reference 

- install style loaders:
`yarn add --dev css-loader vue-style-loader mini-css-extract-plugin`

- add mini-css-extract-plugin to plugins dir

```
const MiniCssExtractPlugin  = require('mini-css-extract-plugin')

//...

plugins: [
  new MiniCssExtractPlugin({
    filename: 'main.css'
  })
]
```

- add babel to support older browsers

`yarn add --dev @babel/core babel-loader @babel/preset-env`

- add loader

```
{
  test: /\.js$/,
  use: 'babel-loader'
}
```

- add .babelrc

```
{
  "presets": [
    ["@babel/env", {
      "modules": false,
      "targets": {
        "browsers": ["> 1%", "last 2 versions", "not ie <= 8"]
      }
    }]
  ]
}
```

- static files `yarn add --dev copy-webpack-plugin`

```
const CopyWebpackPlugin = require('copy-webpack-plugin')
//..
const path = require('path')
function resolve (dir) {
  return path.join(__dirname, '..', dir)
}
plugins: [
  new CopyWebpackPlugin([{
    from: resolve('static/img'),
    to: resolve('dist/static/img'),
    toType: 'dir'
  }])
]
```

### Excercise 3
switch to Vue CLI

[Excercise3 Solved](https://codesandbox.io/s/excercise3-solution-nzcp3)

### Excercise 4

- Create a new project using vue-cli without vue-router or VueX
- Create /views directory and inside Home and Blog component
- Create BaseLayout component that will have header, footer and content slot and register it globally.
- Create DummyNavigator component
- - navigator will get routes object prop
- - when routeChange event triggered navigator will switch displayed component based on provided prop
- - navigator will use history api to change browser url

[Excercise 4 Solution](https://codesandbox.io/s/excercise4-tudnt)

# Day 2
- [Vue router slides](https://slides.com/vladimirnovick/vue-workshop-day-router?token=ec7H5809) Password `Playtech`

### Excercise 5

- Add `vue-router` to our previous exercise project
- Switch `Navigator` component we've created to be a Vue Router
- Add Navigation bar with Nav links using named routes
- Add custom active class to Nav link
- Create `store/store.js` file that will have a post dictionary, getter, and setter. (post should also contain `userId` and `isPublic` flag)
- On the Blog page, display a list of blog posts titles fetched from dummy API and stored in `store.js` post dictionary.
- When clicking on a blog post navigate to Post page with the full post text.
- Create 404 route and catch all unmatched routes there
- Create UserProfile protected page and redirect to Login page when trying to access



