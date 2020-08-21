---
layout: post
title:  JavaScript练习
category: JavaScript
tags: [js基础学习]
---
## HTML
```
<!DOCTYPE html>
<html>
<body>

<h2>外部 JavaScript</h2>

<p id="demo">current time?</p>
<button onclick='document.getElementById("demo").innerHTML=Date()'>现在的时间是？</button>

<!--使用 this.innerHTML 改变自身元素的内容-->
<button onclick="this.innerHTML=Date()">点击显示时间</button>

<a href="javascript:void(0);">点我没有反应的!</a>
<a href="#pos">点我定位到指定位置!</a>

<P>Z
<p id="printZ"></p>
I
<p id="printI"></p>
Q
<p id="printQ"></p>
</P>
E
<p id="printE"></p>
</P>
R
<p id="printR"></p>
</P>
U
<p id="printU"></p>
</P>

FirstName<p id="firstName"></p>
LastName<p id='lastName'></p>
eyeColor<P id='eyeColor'></p>
Age<p id='age'></p>


<button onclick="clickbutton1()">显示弹窗</button>
<button onclick="clickbutton2()">打印日志</button>
<button onclick="timeminus1()">测试倒计时</button>
<p id="timeminustext"></p>
</P>
秒数：
<p id="timeminus"></p>
</P>
<br>
<!-- jQuery Validate -->
<h2><a href="https://www.runoob.com/jquery/jquery-plugin-validate.html">jQuery Validate库</a></h2>
<form class="cmxform" id="commentForm" method="get" action="">
  <fieldset>
    <legend>输入您的名字，邮箱，URL，备注。</legend>
    <p>
      <label for="cname">Name (必需, 最小两个字母)</label>
      <input id="cname" name="name" minlength="2" type="text" required>
    </p>
    <p>
      <label for="cemail">E-Mail (必需)</label>
      <input id="cemail" type="email" name="email" required>
    </p>
    <p>
      <label for="curl">URL (可选)</label>
      <input id="curl" type="url" name="url">
    </p>
    <p>
      <label for="ccomment">备注 (必需)</label>
      <textarea id="ccomment" name="comment" required></textarea>
    </p>
    <p>
      <input class="submit" type="submit" value="Submit">
    </p>
  </fieldset>
</form>
<!-- jQuery Validate -->
<br>
<h2><a href="https://www.jianshu.com/p/b322c2d5d778">Blob测试</a></h2>
<input type="file" accept="image/*" onchange="handleFile(this)"/>
<br>
<!-- <input type="flie" onchange="handleFile(this.files)" />-->
<br>
<img id="upload_image" style="width:200px;height:200px;">
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p id="pos">尾部定位点</p>


<button id="test_ajax_01">获取网站设置</button>
<button id="test_ajax_02">测试登录1</button>
<p id="account_name1"></p>
<button id="test_ajax_03">测试登录2</button>
<button onclick="login_foru22()">测试登录3</button>
<img id="avatar2" />
<p id="test_ajax_text_03"></p>

<script src="https://cdn.staticfile.org/jquery/1.8.3/jquery.min.js"></script>
<!-- jQuery Validate -->
<script src="http://static.runoob.com/assets/jquery-validation-1.14.0/lib/jquery.js"></script>
<script src="http://static.runoob.com/assets/jquery-validation-1.14.0/dist/jquery.validate.min.js"></script>
<!-- jQuery Validate  中文提示-->
<script src="http://static.runoob.com/assets/jquery-validation-1.14.0/dist/localization/messages_zh.js"></script>
<script src="./test.js"></script>
<script src="./my_jquery_function.js"></script>
<!--
<script>
 document.getElementById("printZ").innerHTML = 5 + 6;
</script>
-->
</body>
</html>
```
## JavaScript
```
"use strict"; // 作用是指示 JavaScript 代码应该以“严格模式”执行。详见 https://www.w3school.com.cn/js/js_strict.asp

var x,y;
x= 22;
y= 11;
z= x+y;
var i;
//console 会报错,不允许w在未声明前初始化
//w = 6
//由于javascript数据类型不唯一,person既是对象,又是python 字典(java 集合)
var person = {firstName:"Bill", lastName:"Gates", age:62, eyeColor:"blue"};

function clickbutton1(){
    window.alert('我是一个小弹窗');
}

//打开F12查看console
console.log('打一个日志看看');

document.getElementById("printZ").innerHTML = z;
document.getElementById("printI").innerHTML = i;
document.getElementById("printQ").innerHTML = q;
document.getElementById("firstName").innerHTML = person["firstName"];
document.getElementById("lastName").innerHTML = person["lastName"];
document.getElementById("age").innerHTML = person["age"];
//document.getElementById("eyeColor").innerHTML = person["eyeColor"];
//另一种表现形式
document.getElementById("eyeColor").innerHTML = person.eyeColor;

//Hoisting,提升声明,可以在变量z声明之前使用z
var z;
//Hoisting,只提升声明,不提升初始化,因此test.html中打印的q仍然是undefined
var q=1;

/*=====================let 作用域测试 start============================*/
let t = 5;
function clickbutton2(){
    for (let t = 0; t < 10; t++) {
        // 一些代码...
        console.log('外面的t不影响里面的');
        console.log(t);
    }
}
// 这里输出 i 为 5
console.log('结束循环');
console.log(t);

/*
{
    var r = 8;
    let e = 6; //let 块级作用域
}
document.getElementById("printR").innerHTML = r; // 可以调用r
document.getElementById("printE").innerHTML = e; // 无法调用e,相当于e未声明
*/

/*=====================let 作用域测试 end============================*/

//箭头函数
const u = (x,y) => x*y;
document.getElementById("printU").innerHTML = x + '*' + y + '=' + u(x,y);


/*
   正则表达式 new RegExp(表达式,修饰符)
   修饰符：
   g 表示全局匹配

   表达式：
   ^ 表示以...开头
   $ 表示以...结尾
   + 表示必须包含...
   . 通配符，表示？
       方括号用于查找某个范围内任意一个的字符
           [A-Z] 表示包含大写字母
           [a-z] 表示包含小写字母
           [A-z] 表示包含大写字母和小写字母
           [0-9] 表示包含0-9的数字
           [^abc] 表示不包含a,b,c 三个字符
       (?=.*表达式) 表示必须包含...任意一个
       (?=.量词) 表示必须满足‘量词’对应的含义
   学习网站：
   https://juejin.im/post/5965943ff265da6c30653879
   https://www.liaoxuefeng.com/wiki/1022910821149312/1023021582119488
*/
var str = '1_Qqa@'
var reg1 = new RegExp("^.*(?=.*[0-9])(?=.*[A-Z])(?=.*[a-z])(?=.*\\W)(?=.*[a])(?=.{5}).*$","gm");
var reg2 = /^[a-zA-Z0-9]+$/g;
// 验证 str是否满足reg1
document.write('reg1.test(str): '+reg1.test(str)+'    |');
document.write('str.match(reg1): '+str.match(reg1)+'    |');

/*=====================正则表达式 end============================*/


/*=====================禁用用户调试 start============================*/
//禁用F12
window.onkeydown = window.onkeyup = window.onkeypress = function (event) {
    // 判断是否按下F12，F12键码为123
    if (event.keyCode === 123) {
        event.preventDefault(); // 阻止默认事件行为
        window.event.returnValue = false;
    }
}

// 为右键添加自定义事件，可以禁用
window.oncontextmenu = function() {
    event.preventDefault(); // 阻止默认事件行为
    return false;
}
/*
var threshold = 160; // 打开控制台的宽或高阈值
// 每秒检查一次
setInterval(function() {
    if (window.outerWidth - window.innerWidth > threshold ||
    window.outerHeight - window.innerHeight > threshold) {
        // 如果打开控制台，则刷新页面
        window.location.reload();
    }
}, 1e3);
*/
/*=====================禁用用户调试 end============================*/

//计时事件
//setInterval(function(){alert("Hello")},3000);
/*
  1,点击 - 发送成功，置灰按钮
  2，倒计时60s，显示倒计时，每隔一秒，倒计时-1，
  3，当倒计时为0，显示按钮
*/
var temp
var timeminus = 10
function timeminus1(){
    document.getElementById("timeminustext").innerHTML = '置灰按钮'
    document.getElementById("timeminus").innerHTML = timeminus
    temp =setInterval(function(){myTimer()},1000);
    //setInterval(function(){alert("Hello")},3000);
}
function myTimer(){
    timeminus -= 1
    document.getElementById("timeminus").innerHTML = timeminus
    if (timeminus  == 0){
        clearInterval(temp)
        document.getElementById("timeminustext").innerHTML = '按钮可点击'
        timeminus = 10
    }
}
/*=====================倒计时 end============================*/

/*=====================jQuery Validate =====================*/
$.validator.setDefaults({
    submitHandler: function() {
      alert("提交事件!");
    }
});
$().ready(function() {
    $("#commentForm").validate();
});
/*=====================jQuery Validate =====================*/


/*===================== Blob  =====================*/
//输出选中的文件列表相关的信息
function fileinfo(files) {
    for(var i = 0; i < files.length; i++) {//files是一个类数组对象
        var f = files[i];
        //a.txt 86 text/plain Mon Sep 19 2016 11:07:43 GMT+0800 (中国标准时间)
        console.log(f.name,    //只是名字：没有路径
                    f.size, f.type,    //size和type是Blob的属性
                    f.lastModifiedDate);    //修改时间
    }
}
/*
function handleFile(e) {
      var file = e.files[0];
      var blob = URL.createObjectURL(file);
      var img = document.getElementById("upload_image")[0];
      $("#upload_image").attr("src",blob);
      img.onload = function(e) {
        URL.revokeObjectURL(this.src); //释放createObjectURL创建得对象
      }
    }
*/
//使用promise监听图片加载成功or失败
function get_image_path(e){
  var file = e.files[0];
  var blob = URL.createObjectURL(file);

  return blob;
}
var preloadImage = function (path) {
  return new Promise(function (resolve, reject) {
    var image = new Image();
    image.src = path;
    image.onload  = resolve;
    image.onerror = reject;
  });

};


function handleFile(e) {
  var image_path = get_image_path(e);
  console.log(image_path)
  preloadImage(image_path)
    .then(new Promise(function (resolve, reject) { $("#upload_image").attr("src",image_path); }))
    .then(function () { URL.revokeObjectURL(image_path); },function () { alert('加载失败') })
}
/*===================== Blob  =====================*/
```
[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help