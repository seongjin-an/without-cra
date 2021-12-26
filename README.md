## 1. initialize project
npm init -y
## 2. npm package
// webpack  
npm install --save-dev webpack webpack-dev-server webpack-cli html-webpack-plugin  

// babel   
npm install --save-dev babel-loader @babel/core @babel/preset-env @babel/preset-react @babel/preset-typescript   

// react  
npm install --save react react-dom   

// typescript  
npm install --save @types/react @types/react-dom   
npm install --save-dev typescript ts-loader  

## 3. tsconfig.json
tsc --init  
```
{
  "compilerOptions": {
    "outDir": "./dist",
    "target": "es5",
    "module": "esnext",
    "jsx": "react",
    "noImplicitAny": true,
    "allowSyntheticDefaultImports": true,
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
  },
  "include": [
    "src"
  ]
}
```
## 4. babel.config.js
```
module.exports = {
  presets: ['@babel/preset-react', '@babel/preset-env', '@babel/preset-typescript'],
};
```

## 5. webpack.config.js
```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const webpack = require('webpack');
const mode = process.env.NODE_ENV || 'development';

module.exports = {
  mode,
  devServer: {
    historyApiFallback: true,
    inline: true,
    port: 3000,
    hot: true,
    publicPath: '/',
  },
  entry: {
    app: path.join(__dirname,  'index.tsx'),
  },
 
  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx'],
  },

  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: ['babel-loader', 'ts-loader'],
      },
    ],
  },

	output: {
    path: path.join(__dirname, '/dist'),
    filename: 'bundle.js',
  },

  plugins: [
		new webpack.ProvidePlugin({
      React: 'react',
    }),
    new HtmlWebpackPlugin({
      template: './public/index.html',
    }),
    new webpack.HotModuleReplacementPlugin(),
  ],
};
```
## 6. entry
src/index.tsx
```
import React from 'react';
import ReactDOM from 'react-dom'; 
import App from './src/App';

 
ReactDOM.render( 
 <React.StrictMode> 
  <div>요호</div>
  <App/>
 </React.StrictMode>,
 document.getElementById('root') 
);
```
src/App.tsx
```
import React from 'react'

function App() {
    return (
        <div>
            어~
        </div>
    )
}

export default App
```
public/index.html
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="root"></div> 
   
  </body>
</html>
```

## 7. package.json
```
"scripts": {
    "dev": "webpack server --mode development --open --hot",
    "build": "webpack --mode production",
    //"prestart": "cross-env NODE_ENV=production npm run build",
    //"start": "webpack --mode development"
   "start": "webpack-dev-server --config ./webpack.config.js --mode development", // 추가
  }
```
