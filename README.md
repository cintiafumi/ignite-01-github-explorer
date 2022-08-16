# Setup

## ReactJS

```bash
yarn init -y

yarn add react react-dom
```

Create `/src` and `/public/index.html`

## Babel

```bash
yarn add @babel/core @babel/cli @babel/preset-env -D
```

Create `babel.config.js`

```js
module.exports = {
  presets: [
    '@babel/preset-env'
  ]
}
```

Create `/src/index.js`

```js
const user = {
  name: 'Cintia'
}

console.log(user.address?.street);
```

```bash
yarn babel src/index.js --out-file dist/bundle.js
```

Change content of `/src/index.jsx`

```jsx
import React from 'react'

function App() {
  return <h1>Hello World</h1>
}
```

```bash
yarn add @babel/preset-react -D
```

```js
module.exports = {
  presets: [
    '@babel/preset-env',
    '@babel/preset-react',
  ]
}
```

```bash
yarn babel src/index.jsx --out-file dist/bundle.js
```

## Webpack

```bash
yarn add webpack webpack-cli -D
```

Create `webpack.config.js`

```js
const path = require('path')

module.exports = {
  entry: path.resolve(__dirname, 'src', 'index.jsx'),
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  resolve: {
    extensions: ['.js', '.jsx']
  },
  module: {
    rules: [
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      }
    ]
  }
}
```

```bash
yarn add babel-loader -D
```

Create `/src/App.jsx`

```jsx
export function App() {
  return <h1>Hello World</h1>
}
```

Change `/src/index.jsx`

```jsx
import React from 'react'
import { App } from './App'
```

```bash
yarn webpack
```

## ReactJS structure

`/public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Github Explorer</title>
</head>
<body>
  <div id="root"></div>

  <script src="../dist/bundle.js"></script>
</body>
</html>
```

`/src/index.jsx`

```jsx
import React from 'react'
import { render } from 'react-dom'
import { App } from './App'

render(<h1>Test</h1>, document.getElementById('root'))
```

```bash
yarn webpack
```

Open the `index.html` in a browser.

Remove `import React from 'react'` from `/src/index.jsx` and add `babel.config.js`

```js
module.exports = {
  presets: [
    '@babel/preset-env',
    [
      '@babel/preset-react',
      {
        runtime: 'automatic'
      }
    ]
  ]
}
```

```bash
yarn webpack
```

Change `/src/index.jsx`

```jsx
import { render } from 'react-dom'
import { App } from './App'

render(<App />, document.getElementById('root'))
```

```bash
yarn webpack
```

## Static HTML

Add `html-webpack-plugin`

```bash
yarn add html-webpack-plugin -D
```

Remove `<script src="../dist/bundle.js"></script>` from `index.html`

`webpack.config.js`

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  mode: 'development',
  entry: path.resolve(__dirname, 'src', 'index.jsx'),
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  resolve: {
    extensions: ['.js', '.jsx']
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, 'public', 'index.html')
    })
  ],
  module: {
    rules: [
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      }
    ]
  }
}
```

```bash
yarn webpack
```

A new file `dist/index.html` appears with the script tag.

## Webpack Dev Server

```bash
yarn add webpack-dev-server -D
```

`webpack.config.js`

```js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  mode: 'development',
  entry: path.resolve(__dirname, 'src', 'index.jsx'),
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  resolve: {
    extensions: ['.js', '.jsx']
  },
  devServer: {
    static: path.resolve(__dirname, 'public')
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, 'public', 'index.html')
    })
  ],
  module: {
    rules: [
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      }
    ]
  }
}
```

```bash
yarn webpack serve
```

Open `localhost:8080` in the browser.

Any changes in `App.js` will be automatically updated in the browser.
