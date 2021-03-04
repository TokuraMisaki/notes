# css

## 选择器

``` css
E // 标签选择器
.class // 类选择器
#id  /* id选择器*/
E,F //同时匹配E F元素
E F //匹配属于E后代的F元素
E>F //匹配所有E元素的子元素F
E+F //匹配紧跟E元素的同级F元素
```



## position

``` css
poistion:absolute
// 绝对定位 脱离文档流 相对父级元素定位
position:relative
// 相对定位 相对自身定位 原来的位置依然保留
position:fixed
// 固定定位 父级元素永远是视窗本身
```

居中

``` css
// 上下居中
  position: relative;
  top: 50%;
  transform: translateY(-50%);
// 左右居中
  position: relative;
  left: 50%;
  transform: translate(-50%);
// 水平居中
1. 行内元素 给父元素设置text-align:center
2. 块级元素 给该元素设置margin:0 auto
3. 
```

