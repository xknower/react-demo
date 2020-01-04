# react-demo

> REACT 安装配置 及页面框架案例

## 开发环境

### 1. 安装编辑器

- [VS Code](https://code.visualstudio.com/) - 编辑器

### 2. 配置编辑器

```jsonc
{
  "editor.rulers": [100],
  "editor.formatOnSave": true,
}
```

将以上配置放到 vscode 的用户配置中。

### 3. 安装依赖

```bash

# node & fw
> mkdir react-demo && cd react-demo && npm init -y
> mkdir -p src/
> touch src/index.html
> touch src/index.js
> touch src/main.css
--
> touch webpack.config.js
> touch .babelrc
> touch .gitignore

// fw
├── dist  // 生产目录
│   ├── app.js              // 打包后的app.js
│   └── index.html
│ 
├── src  // 源目录
│   ├── index.html
│   │── index.js           // 源目录入口文件
│   └── main.css
│
├── .babelrc
├── .gitignore
├── package.json
└── webpack.config.js

# package.json
"build": "webpack --mode production",
"dev": "webpack-dev-server --open --mode development"

# webpack
> npm install webpack webpack-cli -D --save-dev
> npm install webpack-dev-server --save-dev
> npm install html-webpack-plugin --save-dev
> config webpack.config.js

// webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin'); 
const webpack = require('webpack');

module.exports = {
  entry: './src/index.js',                      // 入口文件
  output: {                                     // webpack打包后出口文件
    filename: 'app.js',                         // 打包后js文件名称
    path: path.resolve(__dirname, 'dist')       // 打包后自动输出目录
  },
  module: {
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: 'production',
      // 自定义模板
      template: './src/index.html'    
    }),
    // hot 检测文件改动替换 plugin
    new webpack.NamedModulesPlugin(),      
    new webpack.HotModuleReplacementPlugin()    
  ],
  // webpack-dev-server 配置
  devServer: {
    contentBase: './build',
    hot: true
  },
}

# loader
> npm install style-loader css-loader url-loader --save-dev
> npm install babel -g
> npm install babel-core babel-loader@7.1.5 babel-preset-env --save-dev

// config webpack loader
rules: [
  {
    test: /\.css$/,
    use: ['style-loader', 'css-loader']
  },
  {
    test: /\.(png|svg|jpg|gif)$/,
    use: ['url-loader']
  },
  {
    test: /\.(woff|woff2|eot|ttf|otf)$/,
    use: ['url-loader']
  },
  {
    test: /\.(js|jsx)$/,
    exclude: /node_modules/,
    use: ['babel-loader']
  }
]

# react
> npm install babel-preset-react --save-dev
> npm install react react-dom --save-dev

// .babelrc
{
  "presets": ["env", "react"]
}

# 资源文件
// src/index.html (html-webpack-plugin 模板配置)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>

// ./src/index.js
import React from 'react';
import ReactDom from 'react-dom';

import './main.css'

ReactDom.render(
  <h1>hello world</h1>,
  document.getElementById('root')
);
```
