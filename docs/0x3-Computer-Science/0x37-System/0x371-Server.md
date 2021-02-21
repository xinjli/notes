# 0x371 Server

- [1. Backend](#1-backend)
    - [1.1. Node.js](#11-nodejs)
    - [1.2. webpack](#12-webpack)
    - [1.3. Babel](#13-babel)

## 1. Backend
### 1.1. Node.js
Node.js is an runtime extending the V8 engine by adding more features (e.g: file system), 

NPM is its package managing tools. 

The basic commands are as follows:

```bash
npm init # initialize the repository, will create package.json and package_lock.json
npm install <package> # install the package into node_modules and update both package.json
npm install -g <package> # install globally
npm update <package> # updating the local package to most latest compatible versions
npm start # default command run the server.js if existed
npm run <command> # run the customized command defined in the "scripts"
```

### 1.2. webpack
resolve all dependencies in js and  create a single bundled js file

### 1.3. Babel
According to the official site, Babel is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript. It can be tested online here https://babeljs.io/repl
The babel compilation takes three steps:

- Build AST Tree: with babylon parser, jsx -> json tree, demo available here https://astexplorer.net/
- Tree transformation: apply plugins + babel-traverse to transform trees
- Code Generation: generate code with new tree
