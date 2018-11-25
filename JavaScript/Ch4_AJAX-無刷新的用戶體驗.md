# Ch4_AJAX-無刷新的用戶體驗
>* 【Ex4-1 js文件加載時的同步】
```
<html>
 <head>
  <title>async or sync</title>
 </head>
<body>
 <div id="msg"></div>
<script>
       var async= document.createElement('script');
	   //文件內容是: document.getElementById("msg").innerHTML+="async<br/>";
	   async.src='4-1.async.js?r='+Math.random()*99;
	   document.body.appendChild(sync);
</script>
<！--文件內容是document.getElementById("msg").innerHTML+="sync<br/>";-->
<script src="4-1.sync.js"></script>
 </body>
</html>
```
>* 【Ex4-2 最簡單的XML格式】
```
<?xml version="1.0" encoding="UTF-8"?>
<user>
      <name>z3f</name>
	  <homepage>www.z3f.me</homepage>
</user>
```
>* 【Ex4-3 最簡單的JSON格式】
```
("name":"z3f","homepage":"www.z3f.me")
```
>* 【Ex4-4 helloajax】
```

```
