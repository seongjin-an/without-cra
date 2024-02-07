## 1. initialize project
npm init --y
## 2. npm package
// webpack  
npm install --save-dev webpack webpack-dev-server webpack-cli html-webpack-plugin file-loader url-loader css-loader clean-webpack-plugin mini-css-extract-plugin sass-loader style-loader sass copy-webpack-plugin css-minimizer-webpack-plugin

// babel   
npm install --save-dev babel-loader @babel/core @babel/preset-env @babel/preset-react @babel/preset-typescript   

// react  
npm install --save react react-dom   

// typescript  
npm install --save-dev @types/react @types/react-dom   
npm install --save-dev typescript ts-loader ts-node

## 3. tsconfig.json
tsc --init  
```
{
  "compilerOptions": {
    "outDir": "./build",
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
    "typeRoots": ["./node_modules/@types", "./src/types"]
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
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin')
module.exports = {
  mode,
  devServer: {
    historyApiFallback: true,
    // inline: true,
    port: 3000,
    hot: true,
    // publicPath: '/',
  },
  entry: {
    app: path.join(__dirname,  './src/index.tsx'),
  },

  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx'],
  },

  module: {
    rules: [
      {
        test: /\.(ts|tsx)$/,
        use: ['babel-loader', 'ts-loader'],
        // exclude: path.join(__dirname, "/node_modules/")
      },
      {
        test: /\.(png|jpe?g|gif)$/,
        use: [
          {
            loader: 'file-loader',
            options: {
              name: 'assets/[contenthash].[ext]'
            }
          }
        ]
      },
      {
        test: /\.(scss|css)$/,
        use: [{
          loader: MiniCssExtractPlugin.loader,
          options: {
            publicPath: ''
          }
        }, 'css-loader', 'sass-loader']
      }
    ],
  },

  output: {
    path: path.join(__dirname, '/build/static'),
    filename: 'bundle.js',
  },

  plugins: [
    // new webpack.ProvidePlugin({
    //   React: 'react',
    // }),
    new HtmlWebpackPlugin({
      template: './public/index.html',
    }),
    // new webpack.HotModuleReplacementPlugin(),
    new MiniCssExtractPlugin(),
    new CleanWebpackPlugin({
      cleanAfterEveryBuildPatterns: ['build']
    })
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
    "test": "jest",
    "dev": "NODE_ENV=development webpack serve --hot --progress",
    "build": "NODE_ENV=production webpack --progress"
  }
```

## 8. jest install
```
npm i -D @testing-library/jest-dom @testing-library/react @types/jest babel-jest ts-jest
npm i -D jest-environment-jsdom
```

## 9. jest.config.js
```
module.exports = {
    moduleFileExtensions: ['js', 'json', 'jsx', 'ts', 'tsx', 'json'],
    bail: false,
    verbose: true,
    transform: {
        '^.+\\.(js|jsx)?$': 'babel-jest',
        '^.+\\.(ts|tsx)?$': 'ts-jest',
    },
    testEnvironment: 'jsdom',
    moduleNameMapper: {
        '^@/(.*)$': '<rootDir>/$1',
    },
    transformIgnorePatterns: [
        '/node_modules/',
        '^.+\\.module\\.(css|sass|scss)$',
    ],
};
```
