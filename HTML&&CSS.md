## Pure CSS to draw a trapezoid
纯CSS梯形

```
{
    border: 20px solid transparent;
    border-bottom: 20px solid red;
    padding: 0 15px
}
```



## Horizontal Scroll of Page Content
页面内容横向滚动

```
<div class="container">
    <div class="passthrough">
      <div></div>
      <div></div>
      <div></div>
    </div>
</div>

.container{
  display: flex;
}
.passthrough {
  flex: 0 0 auto;
  display: flex;
}
.passthrough > div {
  width: 200px;
  flex: 0 0 auto;
}
```

## Create Gradient Animation Using Background
背景色渐变动画

```
<div class="container"></div>

.container {
  position: relative;
  overflow: hidden;
  width: 300px;
  height: 80px;
  margin: 40px auto;
}

.container::before {
  content: "";
  position: absolute;
  top: -100%;
  left: -100%;
  bottom: -100%;
  right: -100%;
  background: linear-gradient(45deg, #ffc700 0%, #e91e1e 50%, #6f27b0 100%);
  background-size: 100% 100%;
  animation: bgposition 8s infinite linear alternate;
  z-index: -1;
 }

@keyframes bgposition {
  0% {
  transform: translate(30%, 30%);
  }
  25% {
  transform: translate(30%, -30%);
  }
  50% {
  transform: translate(-30%, -30%);
  }
  75% {
  transform: translate(-30%, 30%);
  }
  100% {
  transform: translate(30%, 30%);
  }
}
```

## Different Effects of Line-Height on Mobile Devices

移动端 line-height 不同手机效果不一

```
For containers with a relatively large height, it is better to set the line-height to the height value plus 1px. This approach can achieve good display effects on both Android and iOS platforms.
对于比较大高度的容器，最好把 line-height 设置为高度+1px ，安卓和ios显示都还不错
```

## Ellipsis in One Line
一行省略

```
<div class="demo"></div>

.demo{
    width: 220px;
    display: inline-block;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

## Ellipsis in Multiple Line
多行省略

```
<div class="demo"></div>

.demo{
    display: -webkit-box;    //1.设置display类型为-webkit-box
    font-size: 14px;
    line-height: 18px;
    height: 35px;
    overflow: hidden;        //2.设置元素超出隐藏
    text-overflow: ellipsis; //3.设置超出样式为省略号
    -webkit-line-clamp: 2;   //4.设置2行应用省略
    -webkit-box-orient: vertical;
}
尽量把高度写死， -webkit-line-clamp 属性偶尔成功偶尔失效
```

## Image Filter Effect
图片过滤效果

Some Beautiful Shadow Effects for Images：https://developer.mozilla.org/en-US/docs/Web/CSS/filter

```
<img class="demo">

.demo{
    display: block
    width: 100%
    -webkit-filter drop-shadow(0 8px 7px rgba(0,0,0,.3))
    -moz-filter drop-shadow(0 8px 7px rgba(0,0,0,.3))
    -ms-filter drop-shadow(0 8px 7px rgba(0,0,0,.3))
}
```


## Solve the Issue of Lagging Scrolling on JS Embedded Pages in IOS App
app IOS 中js内嵌页面滑动效果卡顿
```
.scrollView {
    -webkit-overflow-scrolling : touch; // 加上这个IOS顺滑的实现
}
```

## Solutions for Waterfall Flow Layout
瀑布流布局
```
/*
* 使用multi-columns
*/
<div class="masonry">
    <div class="item">
        <div class="item__content"> </div>
    </div>
    <div class="item">
        <div class="item__content"> </div>
    </div> 
    <!-- more items -->
</div>

.masonry { 
    column-count: 5;
    column-gap: 0;
}
.item { 
    break-inside: avoid;
    box-sizing: border-box;
    padding: 10px;
}

/*
* 使用flex
*/
<div class="masonry"> 
    <div class="column">
        <div class="item"> 
            <div class="item__content"></div> 
        </div> 
        <!-- more items --> 
    </div>
    <div class="column">
        <div class="item"> 
            <div class="item__content"></div> 
        </div> 
        <!-- more items --> 
    </div>
</div>

.masonry { 
    display: flex;
    flex-direction: row; 
} 
.column { 
    display: flex;
    flex-direction: column;
    width: calc(100%/2); 
}
```

## CSS for Handling First Line Indentation in Paragraphs
css 段落首行突出
```
<div class="main">
  <p>·Something...</p>
  <p>·Something...</p>
</div>
.main {
  padding-left 5px
}
.main > p {
  text-indent -5px
}
```

## In some rare cases, on certain mobile devices, when the parent element is set to display:flex, the child elements may not be displayed with default flex properties. It is better to manually set the default flex properties for the child elements in such cases.
极个别手机父元素display为flex是子元素没有默认处理flex属性，最好子元素手动设一下默认
```
<div class="main">
  <div :class="child"></div>
</div>
.main {
  display: flex
}
.child {
  flex: 0 0 auto
}
```

















