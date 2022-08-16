# Setup

## React

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
