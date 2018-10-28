---
layout:     post
title:      esLint(用法)
subtitle:   (研究中)
date:       2018-10-28
author:     YC
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - esLint
---

## 前言

vue eslint 代码自动格式化
>vue-cli 代码风格为 JavaScript Standard Style 代码检查规范严格，一不小心就无法运行，使用eslint的autoFixOnSave可以在保存代码的时候自动格式化代码

## 建议阅读
- [vscode推荐阅读](https://link.jianshu.com/?t=https://github.com/varHarrie/Dawn-Blossoms/issues/10)
- [JavaScript Standard Style 代码风格规范](https://link.jianshu.com/?t=https://standardjs.com/readme-zhcn.html)

### 正文 eslint 自动格式化 
```
npm i -g eslint-plugin-vue
#or
npm i -S eslint-plugin-vue
```
创建项目跟路径下的文件：.eslintrc | .eslint.js
复制standard的规则到 .eslintrc 文件中
```
//　添加插件
"plugins": [
    "vue"
]
```
>1、在vscode添加 eslint 插件
>2、在vscode添加 vetur 插件
>3、修改你的setting.json
在你的vscode设置文件里添加：
```
// 添加进你的vscode的 setting.json

"eslint.autoFixOnSave": true,
"eslint.validate": [
    "javascript",{
        "language": "vue",
        "autoFix": true
    },"html",
    "vue"
]
```
### 问题
>1、这样使用能是vscode自动检测到代码不符合的地方 但是和vue-cli3 提供的eslint Standard 风格 有部分规则不能检测
>2、如果vue使用less会对css检测进行报错 因为检测的是标准的css格式而不是less的格式
>3、不能全局配置规则，不然会对老项目疯狂报错

