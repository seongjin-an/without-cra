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
