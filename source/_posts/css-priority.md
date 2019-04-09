---
title: css优先级
date: 2019-04-09 11:45:46
tag: CSS
---

## css权重

* !important: Infinity
* 行间样式:1000
* id:100
* class|属性|伪类:10
* 标签|伪元素:1
* 通配符:0


```css
a{color: yellow;}   /*0001*/
div a{color: green;}  /*0001+0001 =  0002*/
.demo a{color: black;}   /* 0010 + 0001 = 0011 */
.demo input[type="text"]{color: blue;} /*0010+0001+0010 = 0021*/
.demo *[type="text"]{color: grey;} /*0010+0+0010 = 0020*/
#demo a{color: orange;} /*0100+0001 = 0101*/
div#demo a{color: red;} /*0001+0100+0001 = 0102*/

```

