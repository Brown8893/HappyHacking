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
<html>
 <head>
  <title>hello ajax</title>
 </head>
 <body>
	<div id="myajax">hello world!</div>
	<button type="button" id="ajaxBtn">通過 AJAX 改變內容</button>
	<script src="eg.lib.js"></script>
 </body>
</html>
<script>
//定義一個公用的AJAX請求函數
eg.AJAX = function(config,callback){	//接受一個回呼函數和一個配置參數
	var xmlhttp;	//定義一個變數用於後面存儲物件
	if(window.XMLHttpRequest){//如果流覽器支援XMLHttpRequest物件，通常非IE流覽器支持
		xmlhttp = new XMLHttpRequest();
	}else if(window.ActiveXObject){//如果流覽器支援ActiveXObject物件，通常是IE
		try {
			xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");//嘗試創建一個低版本物件，msxml元件2.6版本以下支援
		}
		catch (e){
			try {
				xmlhttp = new ActiveXObject("msxml2.XMLHTTP");//嘗試創建一個高版本物件，msxml元件3.0版本以上支援
			}
			catch (x){
			}
		}
	}
	if(xmlhttp){//如果能夠創建成功，一般都會成功，如果還不行，這系統就重裝吧！太古老了。
		xmlhttp.onreadystatechange = function(){//定義HTTP狀態發生改變時執行的函數
			if (xmlhttp.readyState==4 && xmlhttp.status==200){//當HTTP請求成功時
				callback(xmlhttp.responseText);//把伺服器回應的資料回傳給回呼函數callback
			}
		};
		xmlhttp.open(config.TYPE,config.URL,config.ISASYN);//將傳遞的參數給open方法調用
		xmlhttp.send(config.DATA);//發送AJAX請求
	}
};
(function(){//避免全域污染,將操作放在閉包裡
	var ajaxBtn = eg.$("ajaxBtn");//取得username的DOM對象，eg.$方法定義在eg.lib.js，詳見第2章範例
	                              //給userName物件綁定一個onkeyup事件，eg.addListener方法定義在eg.lib.js，詳見第2章範例
	eg.addListener(ajaxBtn,"click",function(){
		eg.AJAX({TYPE:"GET",//AJAX請求類型
			URL:"4-4.txt",//AJAX請求的URL，該檔只有“hello ajax”字串的純文字
			ISASYN:true//是否非同步
		},function(data){//定義AJAX請求成功後的callback回呼函數
			eg.$("myajax").innerHTML = data;//在元素myajax原本的hello world!會變成hello ajax
		});
	});
})();
</script>
```
>* 【Ex4-5 AJAX同步請求】
```
<html>
 <head>
  <title>hello ajax sync</title>
 </head>
 <body>
	<div id="myajax">hello world!</div>
	<button type="button" id="ajaxBtn">通過 AJAX 同步改變內容</button>
	<script src="eg.lib.js"></script>
 </body>
</html>
<script>
(function(){//避免全域污染,將操作放在閉包裡
	var ajaxBtn = eg.$("ajaxBtn");//取得username的DOM對象，eg.$方法定義在eg.lib.js，詳見第2章範例
	//給userName物件綁定一個onkeyup事件，eg.addListener方法定義在eg.lib.js，詳見第2章範例
	eg.addListener(ajaxBtn,"click",function(){
		eg.AJAX({TYPE:"GET",//AJAX請求類型
			URL:"4-4.txt",//AJAX請求的URL，該檔只有“hello ajax”字串的純文字
			ISASYN:false//是否非同步
		},function(data){//定義AJAX請求成功後的callback回呼函數
			eg.$("myajax").innerHTML = data;//在元素myajax原本的hello world!會變成hello ajax
		});
	});
})();
</script>
```
>* 【Ex4-6 AJAX獲取XML內容】
```

```
