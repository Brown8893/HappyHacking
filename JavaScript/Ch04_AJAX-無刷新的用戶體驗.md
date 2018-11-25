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
<html>
 <head>
  <title>hello ajax xml</title>
 </head>
 <body>
	<div id="myajax">hello world!</div>
	<button type="button" id="ajaxBtn">通過 AJAX 獲取xml內容</button>
	<script src="eg.lib.js"></script>
 </body>
</html>
<script>
(function(){//避免全域污染,將操作放在閉包裡
	var ajaxBtn = eg.$("ajaxBtn");//取得username的DOM對象，eg.$方法定義在eg.lib.js，詳見第2章範例
	//給userName物件綁定一個onkeyup事件，eg.addListener方法定義在eg.lib.js，詳見第2章範例
	eg.addListener(ajaxBtn,"click",function(){
		eg.AJAX({TYPE:"GET",//AJAX請求類型
			URL:"4-6.xml",//AJAX請求的URL，該檔就是範例4-2的代碼
			ISASYN:true//是否非同步
		},function(txt,xml){//定義AJAX請求成功後的callback回呼函數
            var root = xml.getElementsByTagName("name");
			eg.$("myajax").innerHTML =  root[0].childNodes[0].nodeValue;
		});
	});
})();
</script>

```
>* 【Ex4-7 AJAX獲取JSON內容】
```
<html>
 <head>
  <title>hello ajax JSON</title>
 </head>
 <body>
	<div id="myajax">hello world!</div>
	<button type="button" id="ajaxBtn">通過 AJAX 獲取 JSON 內容</button>
	<script src="eg.lib.js"></script>
 </body>
</html>
<script>
(function(){//避免全域污染,將操作放在閉包裡
	var ajaxBtn = eg.$("ajaxBtn");//取得username的DOM對象，eg.$方法定義在eg.lib.js，詳見第2章範例
	//給userName物件綁定一個onkeyup事件，eg.addListener方法定義在eg.lib.js，詳見第2章範例
	eg.addListener(ajaxBtn,"click",function(){
		eg.AJAX({TYPE:"GET",//AJAX請求類型
			URL:"4-7.txt",//AJAX請求的URL，該檔就是範例4-3的JSON代碼
			ISASYN:true//是否非同步
		},function(txt,xml){//定義AJAX請求成功後的callback回呼函數
			var json = new Function("return "+txt)();//簡單的JSON字串轉換為JavaScript物件
			eg.$("myajax").innerHTML = json.name;//輸出用戶名
		});
	});
})();
</script>
```
>* 【Ex4-8 傳統網頁提交】
```
<html>
 <head>
  <title>傳統網頁提交</title>
 </head>
 <body>
  <form method="get" action="4-9.asp" target="_blank">
         <input type="text" name="username" />
		 <input type="submit" value="手動檢查用戶名" />
  </form>
 </body>
</html>
```
>* 【Ex4-9 傳統地檢查用戶名是否已註冊(ASP版)】
```
<%@language="javascript"%>
<%//<%是asp伺服器端運行代碼的起始符號
//@language="javascript"表示本頁面運行的伺服器端預設語言設置為JavaScript
var names = ["z3f","admin","test","anna","cindy","diana"];//定義一個陣列類比資料表示已經註冊過的用戶
//獲取網址傳遞過來的參數username，在JavaScript語法中時時區分大小寫的
var q = Request.QueryString("username");//通過ASP內置物件獲取資料
var has = 0						//定義一個變數用來存儲是否有輸入的用戶名
for (var i=0;i<names.length;i++){	//迴圈比對，一般專案中是查詢資料庫操作
	if(names[i]==q ){			//如果用戶名已存在就標記
		has = 1;					//保存起來
		break;						//退出迴圈
	}
}
if(has == 1){
	Response.Write(q+"已註冊，請換其他用戶名！");//如果找到同名用戶則不能註冊，並通過ASP內置物件輸出
}else{
	Response.Write(q+"還沒有註冊，恭喜你！");//如果沒有同名用戶則可以註冊，並通過ASP內置物件輸出
}
%>
```
>* 【Ex4-10 AJAX檢測用戶名】
```
<html>
 <head>
  <title>AJAX 檢查用戶名</title>
 </head>
 <body>
用戶名：<input type="text" id="username" /><span id="usernameTip"></span>
<script src="eg.lib.js"></script>
 </body>
</html>
<script>
//eg物件已經在eg.lib.js中定義
(function(){//避免全域污染,將操作放在閉包裡
	var userName = eg.$("username");//取得username的DOM對象，eg.$方法定義在eg.lib.js，詳見第2章範例
	var delay;//存儲延遲執行的函數
	var delay2ajax = function(){//AJAX操作部分
		eg.AJAX({TYPE:"GET",//AJAX請求類型
			URL:"4-11.asp?username="+userName.value,//獲取用戶輸入的值並構建AJAX請求的URL
			ISASYN:true//是否非同步
		},function(data){//定義AJAX請求成功後的callback回呼函數
			var json = new Function("return "+data)();//使用簡單的方式把JSON格式的字串文本轉換成JavaScript物件。
			var tip = "";//存儲提示資訊
			if(json.success){//根據服務端定義的成功標誌判斷
				tip = "√ 該用戶名可以註冊";
			}else{
				tip = "× 該用戶名已存在";
			}
			eg.$("usernameTip").innerHTML = tip;//在輸入框旁邊的標籤輸出服務端返回的資訊
		});
	};
	eg.addListener(userName,"keyup",function(){//給userName物件綁定一個onkeyup事件，eg.addListener方法定義在eg.lib.js，詳見第2章範例
		clearTimeout(delay);//如果用戶在短時間內還輸入，則清除要AJAX的操作。
		delay = setTimeout(delay2ajax,800);//重新等待用戶輸入，如果延遲了0.8秒都還沒有輸入，則認為可以自動發起AJAX檢查
	});
})();
</script>
```
>* 【Ex4-11 AJAX檢測用戶名是否註冊(ASP版)】
```
<%@language="javascript"%>
<%//<%是asp伺服器端運行代碼的起始符號
//@language="javascript"表示本頁面運行的伺服器端預設語言設置為JavaScript
var names = ["z3f","admin","test","anna","cindy","diana"];//定義一個陣列類比資料表示已經註冊過的用戶
//獲取網址傳遞過來的參數username，在JavaScript語法中時時區分大小寫的
var q = Request.QueryString("username");//通過ASP內置物件獲取資料
var has = 0						//定義一個變數用來存儲是否有輸入的用戶名
for (var i=0;i<names.length;i++){	//迴圈比對，一般專案中是查詢資料庫操作
	if(names[i]==q ){			//如果用戶名已存在就標記
		has = 1;					//保存起來
		break;						//退出迴圈
	}
}
if(has == 1){
	Response.Write("{success:false}");//如果找到同名用戶則不能註冊，構造成JSON格式字串並通過ASP內置物件輸出
}else{
	Response.Write("{success:true}");//如果沒有同名用戶則可以註冊，構造成JSON格式字串並通過ASP內置物件輸出
}
%>
```
