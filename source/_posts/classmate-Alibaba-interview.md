---
title: 试做同学的阿里前端一面试题
date: 2018-04-09 18:47:15
categories: 技术贴 | 面试题
tags: Javascript
thumbnail: https://pub.wangxuefeng.com.cn/asset/blogthumbnail/classmateAlibabaInterview/thumbnail.png
---

### 【题目1】

```js  
  //请编写一段js函数，该函数的参数是一个骆驼命名法命名的变量标识符，  
  //函数最终返回该标识符的下划线命名法，如，输入：abcDefGh，返回：abc_def_gh
```
> 第一种写法

```js
  function changeName(name){
  	return name.replace(new RegExp(/[A-Z]/, 'g'), (str) => {
  		return '_' + String.fromCharCode(str.charCodeAt(0) | 32);
  	});
  }
```

> 第二种写法

```js
  function changeName(name){
    return name.replace(new RegExp(/[A-Z]/, 'g'), (str) => {
      return `_${str.toLowerCase()}`;
    });
  }

```

### 【题目2】

```js
/**
 * 说明：获取一个数字数组中的最大值
 * 示例：
 * 输入：[1, 5, 3, 9, 2, 7]
 * 输出：9
 */
```

> 第一种写法

```js
function getMaxValue(array){
	return array.sort((a, b) => {
		return b - a;
	})[0];
}
```

> 第二种写法 //ES5

```js
function getMaxValue(array){
  return Math.max.apply(null,array);
}
```

> 第三种写法 //ES6

```js
function getMaxValue(array){
  return Math.max(...array);
}
```

### 【题目3】

```js
/**
 * 多维数组打平成一维数组
 * 说明
 *  1. 数组维度表示数组嵌套数组的深度，如二维数组`[1, [2]]`
 *  2. 数组维度不限，理论上可以无限
 *  3. 数组项可以是number、string、boolean、object、null等JSON合法数据类型
 * 示例：
 *  const a = ['1', 2, false, ['a[b]c', 'd,e,f', [3], [[4]]], [{g: 5}]];
 *  flatten(a); // 返回 ['1', 2, false, 'a[b]c', 'd,e,f', 3, 4, {g: 5}]
 */
```

```js
function flatten(arr){
	return arr.reduce((pre, cur) => {
		return !Array.isArray(cur) ? [...pre,cur] : [...pre,...flatten(cur)];
  },[])
}
```

### 【题目4】

```js
/**
 * 说明：简单实现一个事件订阅机制，具有监听on\one和触发emit方法
 * 示例：
 * const event = new EventEmitter();
 * event.on('someEvent', (...args) => { 
 *     console.log('some_event triggered', ...args);
 * }); 
  * event.one('someEvent', (...args) => { 
 *     console.log('some_event triggered', ...args);
 * }); 
 * event.emit('someEvent', 'abc', '123'); 
 */
 ```

```ts
/**
 * 事件中心
 */
export class EventEmitter {
  event: {
    [any: string]: { func: Function, one: Boolean }[]
  };
  constructor() {
    // 事件池
    this.event = {};
  }

  /**
   * 监听事件
   * @param {String} eventName 事件名称
   * @param {Function} func 事件函数
   * @param {Boolean} one 是否只监听一次
   */
  on(eventName: string, func: Function, one?: Boolean) {
    if (this.event[eventName]) {
      this.event[eventName].push({ func, one });
    } else {
      this.event[eventName] = [{ func, one }];
    }
  }

  /**
   * 监听一次事件
   * @param {String} eventName 事件名称
   * @param {Function} func 事件函数
   */
  one(eventName: string, func: Function) {
    this.on(eventName, func, true)
  }

  /**
   * 解绑事件
   * @param {String} eventName 事件名称
   */
  off(eventName: string) {
    this.event[eventName] = [];
  }

  /**
   * 发送事件
   * @param {String} eventName 事件名称
   * @param {any[]} args 传递的参数
   */
  emit(eventName: string, ...args: any[]) {
    if (!this.event[eventName]) return;
    this.event[eventName].forEach((item, index, array) => {
      item.func(...args);
      if (item.one) {
        array.splice(index, 1);
      }
    });
  }
}

export default new EventEmitter();
```

### 【题目5】

```js
/**
<!DOCTYPE html>
<html>

  <head>
      <meta charset="UTF-8">
      <title>Document</title>
  </head>

  <body>
      <div id="page">
          <div class="content main">
              <div class="refer">
                  <ul>
                      <li></li>
                      <li></li>
                      ...
                  </ul>
              </div>
          </div>
      </div>
      <script>
          var genCssSelector = function () {

          }

          document.addEventListener('click', function (e) {

              //点击li时，返回：html body #page .content.main .refer ul li
              console.log(genCssSelector(e.target));

          })
      </script>
  </body>

</html>
 */
```


```js
var genCssSelector = function (dom) {
	let res = [];
	while(dom.parentNode){
		if(dom.id != ''){
			res.push('#' + dom.id);
		} else if(dom.className != ''){
			let classname = '';
			for (let i = 0, l = dom.classList.length; i < l; i++) {
				classname += '.' + dom.classList[i]
			}
			res.push(classname);
		}else{
			res.push(dom.localName);
		}		
		dom = dom.parentNode;
	}
	return res.reverse().join(' ');
}
```