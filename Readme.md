# Getting Started with React - Development Environment Setup

[React](https://facebook.github.io/react/index.html) is a JavaScript library for building user interfaces developed by Facebook and Instagram.

## Option 1: Clone and Continue

```
git clone --depth=1 https://github.com/praveensewak/react-dev-setup.git
cd react-dev-setup
npm install
```

## Option 2: Manual Setup

Ok, you want to see what's going on here. Following is a basic setup of a development environment with `npm` using `PowerShell` and VS Code on Windows. 

### Setup

We'll setup a couple of packages first:

```
npm init
npm i --save-dev webpack webpack-dev-server babel-cli
npm i --save react react-dom babel-core babel-loader babel-preset-react babel-preset-es2015
```

Create following files and a folder:

```
New-Item index.html -type file
New-Item App.js -type file
New-Item main.js -type file
New-Item webpack.config.js -type file
New-Item build -type directory
```

In the `webpack.config.js` file:

```javascript
module.exports = {
    entry: './main.js',
    output: {
        path: './build',
        filename: 'bundle.js'
    },
    devServer: {
        inline: true,
        port: 3333
    },
    module: {
        loaders: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: 'babel',
                query: {
                    presets: ['es2015', 'react']
                }
            }
        ]
    }
}
```

Put this code in your `index.html`

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>React App!</title>
    </head>
    <body>
        <div id="app"></div>
        <script src="build/bundle.js"></script>
    </body>
</html>
```

In `App.js` (our React component) put this:

```javascript
import React from 'react';

class App extends React.Component {
    render() {
        return <div>Hi There!</div>
    }
}

export default App
```

In `main.js` put this:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('app'))
```

The last thing, in `package.json` file, include this scripts:

```json
...
"scripts": {
    "start": "webpack-dev-server"
}
...
```

### Run

In PowerShell, run:

```
npm start
```

Open browser to http://localhost:3333/.