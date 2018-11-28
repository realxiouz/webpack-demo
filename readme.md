### webpack构建工程(dev及build)

1. 创建项目文件并用npm初始化
  a. `mkdir webpack-demo` -> `cd webpack-demo` -> `npm init -y`
  b. `mkdir src` -> 新建index.js并编辑 `alert('hello webpack')`

2. 安装webpack及webpack-cli
`yarn add webpack webpack-cli -D`

3. 编辑package.json 添加build命令
在scripts字段添加 `"build": "webpack --mode production"`
执行`yarn run build`会在当前目录生成dist目录,并在该目录下生成打包好的main.js

4. 编辑package.json 添加dev命令
  a. 安装webpack-dev-server `yarn add webpack-dev-server -D`
  b. 创建webpack配置文件 `ni webpack.config.js`
  c. 安装HtmlWebpackPlugin插件 `yarn add html-webpack-plugin -D`
  c. 编辑配置文件
  ```
  const HtmlPlugin = require('html-webpack-plugin')
  module.exports = {
    plugins: [
      new HtmlPlugin()
    ]
  }
  ```
  d. 在scripts字段添加  `"dev": "webpack-dev-server --mode development --open --port 9527"`
执行`yarn run dev`会默认打开浏览器

### 构建React项目

1. 添加React依赖
`yarn add react react-dom`

2. 安装babel并添加配置文件
 a. `yarn add @babel/core @babel/preset-env @babel/preset-react -D`
 b. 工程根目录新建`.babelrc`并编辑
 ```
 {
   presets:['@babel/preset-env', '@babel/preset-react']
 }
 ```

3. 安装babel-loader并配置loader
 a. `yarn add babel-loader -D`
 b. 编辑`webpack.config.js`
 ```
 module: {
   rules: [
     {
       test: /\.(js|jsx)$/,
       exclude: '/node_modules/',
       use: 'babel-loader'
     },
     {
       test: /\.css$/,
       use: ['style-loader', 'css-loader']
     }
   ]
 }
 ```

4. 修改index.js并测试
```
import React from 'react'
import ReactDom from 'react-dom'
import './css/index.css'

ReactDom.render(
  <div className='main'>Hello React</div>,
  document.body
)
```
`yarn run dev`
