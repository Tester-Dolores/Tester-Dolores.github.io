---
layout: post
title:  Ajax tips(my_jquery_function.js)
category: JavaScript
tags: [js基础学习]
---
```
/*jQuery（$作为jQuery的简写）
    选择器：
        id选择器： $("#test")
        class选择器： $(".test")
        选择class为intro的p元素： $("p.intro")
        选择第一个p元素： $("p:first")
        选择ul元素的第一个li元素： $("ul.li:first")
        选择带有href属性的元素： $("[href]")
        选择所有target值等于"_blank”的a元素： $("a[target='_blank']")
        选择所有type="button"的input元素和button元素：$(":button")
        选择偶数位置的tr元素：$("tr:even")
        选择奇数位置的tr元素：$("tr:odd")
    事件：
        1.鼠标事件
            触发被选函数的双击事件： $("selector").dblclick()
            添加函数到双击事件（即双击事件发生时运行的函数）：$("selector").dblclick(function)
        2.键盘事件
        3.表单事件
        4.文档/窗口事件
    链： 允许同一元素一条语句运行多个jQuery方法
    遍历
    ajax()方法


    UI测试中可能会应用到的jquery： 元素事件（模拟用户操作），链（模拟用户操作），捕获内容和属性（检查），尺寸
*/
/*
 AJAX
  load() 用于加载资源，并插入到div元素中
  get() post() 用于发请求
*/

API_URL = "https://"

$("#test_ajax_01").click(function(){
    $.ajax({
        url:API_URL + "websites",
        type: "GET",
        success:function(result){
            console.log(result)
            //设置所选元素的文本内容
            $("#test_ajax_text_01").text(JSON.stringify(result));
        }
    });
});

//模拟登录1: 无headers
function login_3d(){
    $.ajax({
        url:API_URL + "login",
        type: "POST",
        contentType: "application/json",
        data:JSON.stringify({
                "account": "test1",
                "password": "123456"
        }),
        success:function(result){
            console.log(result);
            var user_info = result.data.user;
            $("#account_name1").text(user_info.name);
            //设置所选元素的属性
            $("#avatar1").attr("src",user_info.avatar.replace('"','').replace('"',''));
        },
        dataType: "json"
    });
}
$("#test_ajax_02").click(login_3d);

//模拟登录2: 有headers
function login_foru2(){
    $.ajax({
        url:"https://",
        type: "POST",
        contentType: "application/json",
        data:JSON.stringify({
                "email":"test@163.com",
                "password": "123456"
        }),
        success:function(result){
            console.log(result);
            var user_info = result.data.user;
            $("#avatar2").attr("src",user_info.avatar.replace('"','').replace('"',''));
        },
        dataType: "json",
        headers:{
            "content-type":"application/json",
        }
    });
}
$("#test_ajax_03").click(login_foru2);

//测试promise
/*
var p1 = new Promise(function (resolve, reject) {
    console.log('start new Promise...');
});
p1.then(login_3d).then(login_foru2);
*/

//测试ajax与XMLHttpRequest
function login_foru22(){
var xmlhttp;
if(window.XMLHttpRequest){
    xmlhttp = new XMLHttpRequest();
}
else{
    //IE5,IE6不支持XmlHttpRequest
    xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
}
//每当readyState属性改变时，就会调用该函数
xmlhttp.onreadystatechange=function(){
    switch(xmlhttp.readyState){
        case 0:
            console.log("请求未初始化");
            break;
        case 1:
            console.log("服务器连接已建立");
            break;
        case 2:
            console.log("请求已接收");
            break;
        case 3:
            console.log("请求处理中");
            break;
        case 4:
            console.log("请求已完成，且响应已就绪");
            console.log(xmlhttp.responseText);
            break;
    }
}
xmlhttp.open("POST","https://",true);
xmlhttp.setRequestHeader("content-type","application/json");
xmlhttp.send(JSON.stringify({
                "email":"test@163.com",
                "password": "123456"
        }));

}
```
[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help