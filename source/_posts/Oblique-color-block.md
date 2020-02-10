---
title: 斜分色块
date: 2018-07-14 23:47:15
categories: 技术贴 | 面试题
tags: Javascript
---

### 需求描述

  - 将两个色块使用斜线分隔开

### HTML 结构

```html
  <div class="box"></div>
```

### CSS 实现

```css
  .box {
    width: 150px;
    height: 50px;
    position: relative;
    background: pink; /*左边色块的颜色*/
  }
  .box::after {
    position: absolute;
    right: 0;     
    bottom: 0;
    width: 50px; /*右边色块顶部距离右边的距离*/
    border-left: 50px solid transparent; /*右边色块底部距离右边的距离 - 右边色块顶部距离右边的距离*/
    border-bottom: 50px solid deepskyblue; /*右边色块的高度及颜色*/
    content: "";      
  }
```
### 效果预览：

![cssview](https://pub.wangxuefeng.com.cn/asset/blogthumbnail/Oblique-color-block/cssView.png)

### Javascript 封装实现

#### 封装
```javascript
  let Segment = function(opt){
    this.el = document.querySelector(opt.el);
    this.init(opt);
  }

  Segment.prototype = {
    init (opt) {
      this.el.style.position = "relative";    
      this.el.style.width = `${opt.width}px`;
      this.el.style.height = `${opt.height}px`;
      this.el.style.background = opt.leftColor;
      this.drawRight(opt);
    },
    drawRight (opt) {
      document.styleSheets[0].removeRule(`${opt.el}::after`);
      let deg = opt.deg > 90 ? 180 - opt.deg : opt.deg;
      let k = Math.tan(deg * Math.PI/180);  
      let minK = opt.height / opt.width;
      k = k < minK ? minK : k;    
      opt.rightTopWidth = deg != 90 ? opt.width / 2 - opt.height / ( 2 * k) : opt.width / 2;
      let cssRule = [
        `position: absolute`,
        `right: 0`,
        `bottom: 0`,
        `width: ${opt.rightTopWidth}px`,
        `border-left: ${opt.width - 2 * opt.rightTopWidth}px solid transparent`,
        `border-bottom: ${opt.height}px solid ${opt.rightColor}`,
        `content: ""`,
      ];
      opt.deg > 90 ? cssRule.push(`transform: rotateX(180deg);`) : true;
      document.styleSheets[0].insertRule(`${opt.el}::after{${cssRule.join(';')}}`, 0);
    }
  }
```

#### 使用

```javascript
  new Segment({
    el: '.box', // 实例的class或id
    width: 200, // 实例的宽度
    height: 50, // 实例的高都
    leftColor: 'pink', // 左边颜色
    rightColor: 'deepskyblue', // 右边颜色
    deg: 135 // 分割斜线第一象限角的角度
  });
```

### 效果预览：

![jsview](https://pub.wangxuefeng.com.cn/asset/blogthumbnail/Oblique-color-block/jsView.png)

[Github](https://github.com/w-xuefeng/O-ColorBlock)

[预览](https://w-xuefeng.github.io/O-ColorBlock/)



