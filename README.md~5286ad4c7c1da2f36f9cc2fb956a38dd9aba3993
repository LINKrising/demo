# mobile
移动端适配方案及问题解决

# 移动端

## 一、像素

屏幕尺寸：对角线长度，单位英寸，1英寸=2.54厘米

屏幕分辨率：在横纵向上的像素点数，单位px,1px=1像素点。一般分辨率有1080*1920，该像素px不等于css像素（与屏幕分辨率没有关系，是抽象单位，浏览器特有单位，最终转为物理像素），高清屏：相同区域像素点多

像素密度（ppi）

css像素与物理像素：与屏幕特性/用户缩放行为有关

位图像素：32*32:，一个位图像素占据一个物理像素才不会失真或锐化

设备独立像素：是css像素与物理像素转换的重要媒介

像素比：物理像素/设备独立像素，iPhone6像素为2，375**667（设备独立像素），750*1334

750/375=2,1个设备独立像素等于4个物理像素

像素比，设备独立像素，物理像素是设备中的概念，出厂就固定的

**设备独立像素=css像素，width=device-width**,并不在意css像素占据多少物理像素

## 二、视口

布局视口：浏览器主要为980px，一般的pc网页在980px左右，移动端缩放不会改变，pc会改变

视觉视口：用户看到的页面视口，用户缩小就会变，一般：布局视口=视觉视口

理想视口

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>mobile</title>
</head>
<style>
    *{
        margin: 0;
        padding: 0;
    }
    #wrap{
        width: 490px;
        height: 200px;
        background: blueviolet;
    }
</style>
<body>
    <div id="wrap">布局视口占据屏幕一半</div>
</body>
</html>
```

var  layout = document.documentElement.clientWidth（布局视口）

var visual= window.innerWidth（视觉视口）

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>mobile</title>
    <meta name="viewport" content="initial-scale=1.0">
    <!-- 布局视口：375，css像素=设备独立像素 -->
    <!-- 系统缩放参照理想视口，改变的是布局视口 initial-scale=1.0-->
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    #wrap {
        float: left;
        width: 100%;
        height: 200px;
        background: blueviolet;
    }
</style>

<body>
    <div id="wrap"></div>
</body>

</html>
```

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=0.5">
    <!-- 完美视口 谁大听谁的-->
    <title>mobile</title>
</head>
<style>
    *{
        margin: 0;
        padding: 0;
    }
    #wrap{
        width: 375px;
        height: 200px;
        background: blueviolet;
    }
</style>
<body>
    <div id="wrap">
        linklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklinklink
    </div>
</body>
</html>
```

## 三、适配方案

### 1.rem适配



```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    *{
        margin: 0;
        padding: 0;
    }
    #wrap{
        width: 16rem;
        height: 10rem;
        background: blueviolet;
    }
</style>
<body>
    <div id="wrap">
        
    </div>
    <script>
        //改变元素在不同设备上css像素个数
        ~~((num)=>{
            const styleNode = document.createElement('style')
            const w = document.documentElement.clientWidth / num
            styleNode.innerText = `html{font-size:${w}px!important}`
            document.head.appendChild(styleNode)
        })(16)

    </script>
</body>
</html>
```

### 2.viewport适配

所量即所得

没有实现完美视口

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    #wrap {
        width: 200px;
        height: 200px;
        background: blueviolet;
    }
</style>

<body>
    <div id="wrap">

    </div>
    <script>
        //将布局视口变为设计图宽度,元素css像素不变
        ~~((yourWidth) => {
            const designWidth = yourWidth
            const scale = document.documentElement.clientWidth / designWidth
            const viewport = document.querySelector('meta[name="viewport"]')
            viewport.content = `initial-scale=${scale},minimum-scale=${scale},maximum-scale=${scale}`
        })(640)

    </script>
</body>

</html>
```

## 四、1物理像素解决方案

### 1.淘宝方案

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    #wrap {
        width: 16rem;
        height: 1px;
        margin-top: 50px;
        background: blueviolet;
    }
</style>

<body>
    <div id="wrap">

    </div>
    <script>
        //改变元素在不同设备上css像素个数
        ~~((num) => {
            const dpr = window.devicePixelRatio || 1
            const styleNode = document.createElement('style')
            const w = document.documentElement.clientWidth * dpr / num
            styleNode.innerText = `html{font-size:${w}px!important}`
            document.head.appendChild(styleNode)

            const scale = 1 / dpr
            const viewport = document.querySelector('meta[name="viewport"]')
            viewport.content = `initial-scale=${scale},minimum-scale=${scale},maximum-scale=${scale}`



        })(16)       
    </script>
</body>

</html>
```

### 2.css3方案

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    #wrap {
        width: 16rem;
        height: 1px;
        margin-top: 50px;
        background: blueviolet;
    }

    @media only screen and (-webit-device-pixel-ratio:2) {
        #wrap {
            transform: scaleY(.5)
        }
    }

    @media only screen and (-webit-device-pixel-ratio:3) {
        #wrap {
            transform: scaleY(.33333)
        }
    }
</style>

<body>
    <div id="wrap">

    </div>
    <script>
        //改变元素在不同设备上css像素个数
        ~~((num) => {
            const styleNode = document.createElement('style')
            const w = document.documentElement.clientWidth / num
            styleNode.innerText = `html{font-size:${w}px!important}`
            document.head.appendChild(styleNode)
        })(16)

    </script>
</body>

</html>
```

## 五、query问题

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    .item {
        width: 200px;
        height: 200px;
        margin-top: 20px;
    }
</style>

<body>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <script>
        //query静态列表获取后dom结构发生改变就不行了，需要重新获取
        /*
            let items = document.querySelectorAll('.item')
            document.body.innerHTML+='<div class="item"></div>'
            items = document.querySelectorAll('.item')
            for(let i=0;i<items.length;i++){
                items[i].style.background = 'red'
            }
        */
        let items = document.getElementsByClassName('item')
        document.body.innerHTML += '<div class="item"></div>'
        for (let i = 0; i < items.length; i++) {
            items[i].style.background = 'red'
        }
    </script>
</body>

</html>
```

## 六、移动端基础事件

### 1.默认事件阻止

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    #wrap {
        width: 200px;
        height: 200px;
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        margin: auto;
        background: blueviolet;
        line-height: 200px;
        text-align: center;
    }
    #inner{
        height: 50px;
        width: 50px;
    }
</style>

<body>
    <div id="wrap">
        <div id="inner">
            <div id="inner">
                inner
            </div>
        </div>
    </div>
    text
    <script>
        /*
            touchstart
            touchmove
            touchend

            长按复制等问题，决定阻止事件默认行为
            浏览器(不能document阻止)跟//真机有问题
        */
        window.onload = function () {
            document.addEventListener('touchstart', (ev) => {
                ev = ev || event
                console.log(ev.cancelable)
                ev.preventDefault()
            })
            const wrap = document.querySelector('#wrap')
            const inner = document.querySelector('#inner')
            wrap.addEventListener('touchstart', (ev) => {
                ev = ev || event
                console.log('touchstart')
            })
            wrap.addEventListener('touchmove', () => {
                console.log('touchmove')
            })
            wrap.addEventListener('touchend', () => {
                console.log('touchend')
            })
            inner.addEventListener('touchstart', (ev) => {
                ev = ev || event
                ev.stopPropagation();
                console.log('touchstart')
            })
        }

    </script>
</body>

</html>


```

### 2.禁止菜单

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    #wrap {
        width: 200px;
        height: 200px;
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        margin: auto;
        background: blueviolet;
        line-height: 200px;
        text-align: center;
    }

    #inner {
        width: 100px;
        height: 100px;
        position: absolute;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        margin: auto;
        background: black;
        line-height: 100px;
        text-align: center;
    }

</style>

<body>
    <div id="wrap">
        <div id="inner">
            inner
        </div>
    </div>
    <script>
        /*
            touchstart
            touchmove
            touchend
        */
        window.onload = function () {
            const wrap = document.querySelector('#wrap')
            const inner = document.querySelector('#inner')
            document.oncontextmenu = () => {
                return false
            }
            wrap.oncontextmenu = (ev) => {
                ev = ev || event
                ev.stopPropagation()
            }
            inner.oncontextmenu = (ev) => {
                return false
            }


        }

    </script>
</body>

</html>
```



### 3.自定义菜单

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    #menu {
        position: absolute;
        width: 100px;
        height: 400px;
        background: red;
        display: none;
    }
</style>

<body>
    <div id="menu">

    </div>
    <script>
        /*
            touchstart
            touchmove
            touchend
        */
        window.onload = function () {
            const menu = document.querySelector('#menu')
            document.oncontextmenu = (ev) => {
                ev = ev || event
                let x = ev.clientX
                let y = ev.clientY
                menu.style.left = x+'px'
                menu.style.top = y+'px'
                menu.style.display = 'block'
                return false
            }
            document.onclick = ()=>{
                menu.style.display = 'none'

            }



        }

    </script>
</body>

</html>
```

### 4.一个隐患

### 5.pc端事件点透问题·

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    #wrap {
        width: 14rem;
        height: 10rem;
        background: blueviolet;
    }
    a{
        position: absolute;
        top: 0;
        left: 0;
    }
</style>

<body>
    <div id="wrap"></div>
    <a href="http://www.baidu.com">baidu</a> 
    <script>
        //1.pc端事件可以在移动端触发
        //2.pc端事件有默认的300ms延迟

        window.onload = function () {
            const wrap = document.querySelector('#wrap')
            document.addEventListener('touchstart', (ev) => {
                ev = ev || event
                console.log(ev.cancelable)
                ev.preventDefault()
            })
            ~~((num) => {
                const styleNode = document.createElement('style')
                const w = document.documentElement.clientWidth / num
                styleNode.innerText = `html{font-size:${w}px!important}`
                document.head.appendChild(styleNode)
            })(16)
            wrap.onclick = ()=>{
                wrap.style.display = 'none'
            }
        }

    </script>
</body>

</html>
```

### 6.移动端a处理

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }


</style>

<body>
    <a href="http://www.baidu.com">baidu</a> <a href="http://www.baidu.com">baidu</a><a href="http://www.baidu.com">baidu</a>
    <script>
        //1.pc端事件可以在移动端触发
        //2.pc端事件有默认的300ms延迟

        window.onload = function () {
            const aNodes = document.querySelectorAll('a')
            document.addEventListener('touchstart', (ev) => {
                ev = ev || event
                console.log(ev.cancelable)
                ev.preventDefault()
            })
            ~~((num) => {
                const styleNode = document.createElement('style')
                const w = document.documentElement.clientWidth / num
                styleNode.innerText = `html{font-size:${w}px!important}`
                document.head.appendChild(styleNode)
            })(16)
            for(var i=0;i< aNodes.length;i++){
                aNodes[i].addEventListener('touchstart', function () {
                    this.isMoved = false

                })
                aNodes[i].addEventListener('touchmove', function () {
                    this.isMoved = true

                })                
                aNodes[i].addEventListener('touchend',function(){
                    if(!this.isMoved){
                    location.href = this.href
                    }

                })
            }
        }

    </script>
</body>

</html>
```

### 7.事件属性与方法

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }

    #wrap {

        width: 200px;
        height: 400px;
        background: red;

    }
</style>

<body>
    <div id="wrap">

    </div>
    <script>
        /*
            touchstart
            touchmove
            touchend

            changedTouches 触发当前事件的手指列表
            targetTouches 触发当前事件时元素上的手指列表
            touches 触发当前事件时屏幕上的手指列表

        */
        const wrap = document.querySelector('#wrap')
        wrap.addEventListener('touchend',(ev)=>{
            ev = ev||event
            console.log(ev)
            wrap.innerHTML= "changedTouches"+ev.changedTouches.length+'<br/>'
            wrap.innerHTML += "targetTouches" + ev.targetTouches.length + '<br/>'
            wrap.innerHTML += "touches" + ev.touches.length
        })



    </script>
</body>

</html>
```

### 8.常见问题

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <!--tel email-->
    <meta name="format-detection" content="telephone=no,email=no">
    <title>mobile</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }
    a{
        text-decoration: none;
        -webkit-tap-highlight-color: rgba(0,0,0,0)
    }

    #wrap {

        width: 200px;
        height: 400px;
        background: red;

    }
    #btn{
        width: 20px;
        height: 20px;
        -webkit-appearance: none;
    }
    p{
        font-size: 22px;
        max-height: 99999px;
    }

   
</style>

<body>
    <div id="wrap">
        <a href="tel:130">130</a>
        <a href="mailto:133@qq.com">133@qq.com</a>
        <button id="btn">btn</button>
        <!--圆角会很圆-->
        <p>1</p>
        <p>2</p>
        <p>3</p>
        <p>4</p>
        <p>5</p>
        <!--浏览器会智能放大字体 font boosting-->
    </div>
    <script>


    </script>
</body>

</html>
```


