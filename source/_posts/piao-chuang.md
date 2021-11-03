---
title: '飘窗'
date: 2019-11-21 11:15:30
tags: []
published: true
hideInList: false
feature: 
---
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <!--飘窗-->
    <div id="roll">
      <div class="title">
        通知
      </div>
      <div class="content">
        自2019年9月29日起，取消 <span>河南省二级建造师临时执业证书</span> ，不再办理临时二级建造师各项注册业务。临时二级建造师申请的安管人员证书不再延续，不需进行继续教育。
      </div>
    </div>
    <style>
      #roll {
        /* height: 460px; */
        width: 460px;
        position: fixed; /*fixed实现绝对定位*/
        cursor: pointer;
        background-color: aliceblue;
        padding: 20px 20px 30px 20px;
        box-shadow: 0 0 20px #ccc;
        z-index: 99;
      }
      #roll .title{ text-align: center; font-size: 24px; margin-bottom: 20px; }
      #roll .content{  font-size: 18px; text-indent: 2em; line-height: 1.6; text-align: justify; } 
      #roll .content span{ color: #f33;  font-style: italic;  } 
    </style>
    <script>
      var ggRoll = {
        //创建对象直接量
        roll: document.getElementById("roll"), //获取id属性为roll的对象
        speed: 20, //飘动速度，即为定时器函数多长时间执行一次
        statusX: 1, //规定每执行一次函数，left属性值变化的幅度
        statusY: 1, //规定每执行一次函数，top属性值变化的幅度
        x: 100, //规定初始状态下left属性的值
        y: 300, //规定初始状态下top属性的值
        //差值用来测算left属性值的极限
        winW: function(){  
         return document.documentElement.clientWidth -
         this.roll.offsetWidth
        },
        //差值用来测算top属性值的极限
        winH:function(){
         return document.documentElement.clientHeight -
         this.roll.offsetHeight
        },
        //声明函数
        Go: function() {
          //设置div的left属性值
          this.roll.style.left = this.x + "px";
          //设置div的top属性值
          this.roll.style.top = this.y + "px";
          //如果statusX=1则每次减少1px,否则减少1px
          this.x = this.x + (this.statusX ? -1 : 1);
          //如果left属性值小于0，也就是div要超出左边界了，就将statusX设置为0
          if (this.x < 0) {
            this.statusX = 0;
          }
          //如果top属性值大于winW，也就是div要超出右边界了，就将statusX设置为1
          if (this.x > this.winW()) {
            this.statusX = 1;
          }

          this.y = this.y + (this.statusY ? -1 : 1);
          if (this.y < 0) {
            this.statusY = 0;
          }
          if (this.y > this.winH()) {
            this.statusY = 1;
          }
        }
      };

      var interval = setInterval("ggRoll.Go()", ggRoll.speed); 
      ggRoll.roll.onmouseover = function() { 
        clearInterval(interval);
      }; //onmouseover属性：鼠标移动到元素上时触发
      ggRoll.roll.onmouseout = function() {
        interval = setInterval("ggRoll.Go()", ggRoll.speed);
      }; //onmouseout属性:鼠标离开元素时触发
      // window.onresize = function(){ 
      //   clearInterval(interval);
      //   interval = setInterval("ggRoll.Go()", ggRoll.speed); 
      // }
    </script>
  </body>
</html>

```
```js
      class PiaoChuang {
        constructor(id) {
          this.interval = null;
          this.id = id;
          this.roll = document.getElementById(this.id);
          this.speed = 20; //飘动速度，即为定时器函数多长时间执行一次
          this.statusX = 1; //规定每执行一次函数，left属性值变化的幅度
          this.statusY = 1; //规定每执行一次函数，top属性值变化的幅度
          this.x = 100; //规定初始状态下left属性的值
          this.y = 300; //规定初始状态下top属性的值
        }
        init(){
          this.interval = setInterval(this.Go.bind(this), this.speed);
          //onmouseover属性：鼠标移动到元素上时触发
          this.roll.onmouseover = ()=>{
            clearInterval(this.interval);
          };
          //onmouseout属性:鼠标离开元素时触发
          this.roll.onmouseout = ()=>{
            this.interval = setInterval(this.Go.bind(this), this.speed);
          };
        }
        //差值用来测算left属性值的极限
        winW() {
          return document.documentElement.clientWidth - this.roll.offsetWidth;
        }
        //差值用来测算top属性值的极限
        winH() {
          return document.documentElement.clientHeight - this.roll.offsetHeight;
        }
        Go() {
          //设置div的left属性值
          this.roll.style.left = this.x + "px";
          //设置div的top属性值
          this.roll.style.top = this.y + "px";
          //如果statusX=1则每次减少1px,否则减少1px
          this.x = this.x + (this.statusX ? -1 : 1);
          //如果left属性值小于0，也就是div要超出左边界了，就将statusX设置为0
          if (this.x < 0) {
            this.statusX = 0;
          }
          //如果top属性值大于winW，也就是div要超出右边界了，就将statusX设置为1
          if (this.x > this.winW()) {
            this.statusX = 1;
          }

          this.y = this.y + (this.statusY ? -1 : 1);
          if (this.y < 0) {
            this.statusY = 0;
          }
          if (this.y > this.winH()) {
            this.statusY = 1;
          }
        }
      }
      const piaochuang = new PiaoChuang("roll"); 
      piaochuang.init()
```