---
title: React学习记录
date: 2019-04-19 15:08:17
categories: React
tags: react
---
### 运行yarn eject出现问题
    解决：运行`npm install`, 或者删除node_modules后重新运行 `npm/cnpm install`

### React配置文件释放后按需导入antd

在运行yarn eject 后按需导入antd:

  1. 运行 `yarn add babel-plugin-import`
  2. 在package.json中添加 
  ```json 
  "babel": {
    "presets": [
      "react-app"
    ],
    "plugins": [
      [
        "import",
        {
          "libraryName": "antd",
          "style": "css"
        }
      ]
    ]
  }```
  3. 
