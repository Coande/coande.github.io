title: JavaScript计算器
date: 2015-08-06 21:21:03
tags:
	- JavaScript
categories:
	- 技巧
---
刚学JavaScript，写了个简易整数计算器。我的得意之作哈，勿喷~<!--more-->
```
<!DOCTYPE html>
<html>
 <head>
  <title> 事件</title>  
  <script type="text/javascript">
   function count(){
    //获取第一个输入框的值
    var txt1=parseInt(document.getElementById("txt1").value);
	//获取第二个输入框的值
    var txt2=parseInt(document.getElementById("txt2").value);
	//获取选择框的值
    var select=document.getElementById("select").value;
	//获取通过下拉框来选择的值来改变加减乘除的运算法则
    var result;
    switch(select)
    {
        case "+":
            result=txt1+txt2;
            break;
        case "-":
            result=txt1-txt2;
            break;
        case "*":
            result=txt1*txt2;
            break;
        case "/":
            result=txt1/txt2;
    }
    //设置结果输入框的值 
    document.getElementById("result").value=result;
   }
  </script> 
 </head> 
 <body>
   <input type='text' id='txt1' /> 
   <select id='select'>
		<option value='+'>+</option>
		<option value="-">-</option>
		<option value="*">*</option>
		<option value="/">/</option>
   </select>
   <input type='text' id='txt2' /> 
   <input type='button' value=' = ' onclick="count()"/> <!--通过 = 按钮来调用创建的函数，得到结果--> 
   <input type='text' id='result' />   
 </body>
</html>
```
效果：

<script type="text/javascript">
   function count(){
    //获取第一个输入框的值
    var txt1=parseInt(document.getElementById("txt1").value);
	//获取第二个输入框的值
    var txt2=parseInt(document.getElementById("txt2").value);
	//获取选择框的值
    var select=document.getElementById("select").value;
	//获取通过下拉框来选择的值来改变加减乘除的运算法则
    var result;
    switch(select)
    {
        case "+":
            result=txt1+txt2;
            break;
        case "-":
            result=txt1-txt2;
            break;
        case "*":
            result=txt1*txt2;
            break;
        case "/":
            result=txt1/txt2;
    }
    //设置结果输入框的值 
    document.getElementById("result").value=result;
   }
  </script> 
 
  <input type='text' id='txt1' /> <select id='select'>
		<option value='+'>+</option>
		<option value="-">-</option>
		<option value="*">*</option>
		<option value="/">/</option>
   </select> <input type='text' id='txt2' /> <input type='button' value=' = ' onclick="count()"/><!--通过 = 按钮来调用创建的函数，得到结果--> <input type='text' id='result' />