# jQuery 語法
```
jQuery 語法是通過選取 HTML 元素，並對選取的元素執行某些操作。

基礎語法： $(selector).action()

美元符號定義 jQuery
選擇符（selector）"查詢"和"查找" HTML 元素
jQuery 的 action() 執行對元素的操作

實例:
$(this).hide() - 隱藏當前元素
$("p").hide() - 隱藏所有 <p> 元素
$("p.test").hide() - 隱藏所有 class="test" 的 <p> 元素
$("#test").hide() - 隱藏所有 id="test" 的元素
```

## 範例一
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js">
</script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("#div1").fadeIn();
    $("#div2").fadeIn("slow");
    $("#div3").fadeIn(3000);
  });
});
</script>
</head>

<body>
<p>實例演練 fadeIn() 使用了不同參數的效果。</p>
<button>點擊淡入 div 元素。</button>
<br><br>
<div id="div1" style="width:80px;height:80px;display:none;background-color:red;"></div><br>
<div id="div2" style="width:80px;height:80px;display:none;background-color:green;"></div><br>
<div id="div3" style="width:80px;height:80px;display:none;background-color:blue;"></div>

</body>
</html>
```
### 使用CDN
```
<script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js">

```

## 範例二
```
<html>
<head>
<script type="text/javascript" src="/jquery/jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $(".btn1").click(function(){
  $("p").fadeOut()
  });
  $(".btn2").click(function(){
  $("p").fadeIn();
  });
});
</script>
</head>
<body>
<p>This is a paragraph.</p>
<button class="btn1">Hide</button>
<button class="btn2">Show</button>
</body>
</html>
```

## 範例三
```
資料來雲:http://www.w3school.com.cn/jquery/jquery_animate.asp
```
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script> 
$(document).ready(function(){
  $("button").click(function(){
    var div=$("div");  
    div.animate({left:'100px'},"slow");
    div.animate({fontSize:'3em'},"slow");
  });
});
</script> 
</head>

<body>

<button>開始動畫</button>
<p>預設情況下，所有 HTML 元素的位置都是靜態的，並且無法移動。如需對位置進行操作，記得首先把元素的 CSS position 屬性設置為 relative、fixed 或 absolute。</p>
<div style="background:#98bf21;height:100px;width:200px;position:absolute;">HELLO</div>

</body>
</html>
```


## 範例四_登入的畫面 index.html
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
	<title>T-shirt 王的行動網站</title>
	<link rel="stylesheet" href="http://code.jquery.com/mobile/1.4.5/jquery.mobile-1.4.5.min.css" />
    <script src="http://code.jquery.com/jquery-2.2.3.min.js"></script>
    <script src="http://code.jquery.com/mobile/1.4.5/jquery.mobile-1.4.5.min.js"></script>    
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<script>
	  var i = 0;
      var img = new Array("piece1.jpg", "piece2.jpg", "piece3.jpg");
      var msg = new Array("「喬巴」－夢想成為能治百病的神醫。", 
	    "「索隆」－夢想成為世界第一的劍士。", 
		"「佛朗基 」－傳說中的船匠湯姆的弟子，打造了千陽號。"); 
	  function prev(){
	    i--; 
	    if (i < 0) {i = 2;}
	    $("#roleimg").attr("src", img[i]);		
		$("#rolemsg").text(msg[i]);
      }
	  function next(){
	    i++; 
	    if (i > 2) {i = 0;}
	    $("#roleimg").attr("src", img[i]);		
		$("#rolemsg").text(msg[i]);
      }
	</script>
  </head>
  <body>  
  //整個網頁==使用data-role="page"   網頁id="home"
    <div data-role="page" id="home">
   //表頭===使用data-role="header"
      <div data-role="header" data-position="fixed">  
 	    <h1>T-shirt 王</h1>
      </div>
   //內容==使用  data-role="content"
      <div data-role="content">	    
		<img src="piece.jpg" width="100%"> 
	    <a href="#story" data-rel="dialog" data-role="button" data-icon="arrow-r">故事介紹</a>
		<a href="#role" data-role="button" data-icon="arrow-r">角色介紹</a>
		<a href="http://www.ttv.com.tw/drama/2005/cartoon/onepeace/01-story.htm" data-rel="external" data-role="button" data-icon="arrow-r">航海王官方網站</a>
	  </div>	  
   //表頭===使用data-role="header"	  
   //小測驗:: data-position="fixed"
      <div data-role="footer" data-position="fixed">
	    <h4>&copy;快樂Docker</h4>
	  </div>
    </div>
 
 //定義story
     <div data-role="page" id="story">
	  <div data-role="header">
	    <h1>Docker介紹</h1>	            
      </div>
      <div data-role="content">
        <p>海賊王Docker遺留下一個被稱為ONEPIECE的神秘寶藏，
        而主角「LUFU Docker」找了海盜剋星「So long Docker」、女賊「na mei Docker」、
        可愛馴鹿「chifu Docker」等幾位夥伴要一起尋找傳說中的寶藏。</p>
      </div>
	</div>
 //定義role	
	<div data-role="page" id="role">
	  <div data-role="header">
	    <h1>人物介紹</h1>	            
      </div>
      //第一個腳色
	  <div data-role="content">
	    <img id="roleimg" src="piece1.jpg" width="100%">
		<p id="rolemsg">「chou ba dcoker」－夢想成為能治百病的神醫。</p>
	  </div>
	  <div data-role="footer" data-position="fixed">
	    <div data-role="navbar">
	      <ul>
            <li><a href="#home" class="ui-btn-active ui-state-persist">回首頁</a></li>
            <li><a href="javascript:prev();">上一個</a></li>
            <li><a href="javascript:next();">下一個</a></li>
          </ul>
	    </div>  
      </div>
	</div>	
  </body>
</html>
```
