# Setup

```bash
yarn init -y

yarn add react react-dom
```

Create `/src` and `/public/index.html`

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
