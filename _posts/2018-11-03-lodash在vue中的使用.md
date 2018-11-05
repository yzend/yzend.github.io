---
layout:     post
title:      lodash(用法)
subtitle:   (持续中)
date:       2018-11-03
author:     YC
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - lodash
---

## 前言

vue lodash 使用
>lodash 是一套工具库 它内部封装了许多对字符串、数组、对象、常见数据类型的处理函数，其中部分是目前Es尚未定制的规范，但同时被业界认可的辅助函数。本文章记载的是一些个人觉得比较常用的函数 已经在vuecli 中安装使用


## 建议阅读
- [lodash中文文档](http://www.css88.com/doc/lodash/)

### 正文 在vue中使用lodash

## 一、安装
```
cnpm i lodash -S
#or
yarn add lodash
```
## 二、引入vue
```
import _ from 'lodash'
Vue.use(_)
```
在vue-cli3中eslint 会对_报错
在package.json中添加全局标实
```
"eslintConfig": {
    "globals": {
        "_": true
    }
}
```

>在vue组件中直接调用 _

### 常用工具

##对象 Object

> 1、_.pick(object, [props])
创建一个从 object 中选中的属性的对象。 类似与查找功能 在一个对象中找出想要的key以及对应的键值 
* 参数
* object (Object): 来源对象。
* [props] (...(string|string[])): 要被忽略的属性。 （查找key 的 字符串数组）
* 返回
* (Object): 返回新对象。

例子：
```
var object = { 'a': 1, 'b': '2', 'c': 3 };
_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```
##数组 Array
>1、_.indexOf(array, value, [fromIndex=0])

##集合 Collection
>1、_.groupBy(collection, [iteratee=_.identity])
创建一个对象，key 是 iteratee 遍历 collection(集合) 中的每个元素返回的结果。 
分组值的顺序是由他们出现在 collection(集合) 中的顺序确定的。每个键对应的值负责生成 key 的元素组成的数组。iteratee 调用 1 个参数： (value)。
* 参数
* collection (Array|Object): 一个用来迭代的集合。
* [iteratee=_.identity] (Array|Function|Object|string): 这个迭代函数用来转换key。 (筛选参数 用来查找集合里的正确的数据)
* 返回
* (Object): 返回一个组成聚合的对象。
```
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }
 
返回一个true和false的对象集合

_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

##函数 Function
>1、_.throttle(func, [wait=0], [options={}])
创建一个节流函数，在 wait 秒内最多执行 func 一次的函数。 该函数提供一个 cancel 方法取消延迟的函数调用以及 flush 方法立即调用。 可以提供一个 options 对象决定如何调用 func 方法， options.leading 与|或 options.trailing 决定 wait 前后如何触发。 func 会传入最后一次传入的参数给这个函数。 随后调用的函数返回是最后一次 func 调用的结果。 

*注意: 如果 leading 和 trailing 都设定为 true 则 func 允许 trailing 方式调用的条件为: 在 wait 期间多次调用。 

*如果 wait 为 0 并且 leading 为 false, func调用将被推迟到下一个点，类似setTimeout为0的超时。
*参数
*func (Function): 要节流的函数。
*[wait=0] (number): 需要节流的毫秒。
*[options={}] (Object): 选项对象。
*[options.leading=true] (boolean): 指定调用在节流开始前。
*[options.trailing=true] (boolean): 指定调用在节流结束后。
*返回
*(Function): 返回节流的函数。

```
// 避免在滚动时过分的更新定位
jQuery(window).on('scroll', _.throttle(updatePosition, 100));
 
// 点击后就调用 `renewToken`，但5分钟内超过1次。
var throttled = _.throttle(renewToken, 300000, { 'trailing': false });
jQuery(element).on('click', throttled);
 
// 取消一个 trailing 的节流调用。
jQuery(window).on('popstate', throttled.cancel);
```

* 在vue中的使用
```
methods: {
    sendMessage: _.throttle(function (newVal) {
        if (typeof (JSON.stringify(newVal)) === 'string') {
            this.$chat.send({
                chat: JSON.stringify(newVal)
            })
        }
    }, 100)
}
watch: {
    imgObj: {
      handler: function (newVal, oldVal) {
        this.sendMessage(newVal)
      },
      deep: true
    }
}
```



### 问题
>1、这样使用能是vscode自动检测到代码不符合的地方 但是和vue-cli3 提供的eslint Standard 风格 有部分规则不能检测
>2、如果vue使用less会对css检测进行报错 因为检测的是标准的css格式而不是less的格式
>3、不能全局配置规则，不然会对老项目疯狂报错

