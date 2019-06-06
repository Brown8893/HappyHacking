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
      var msg = new Array("Docker是一個開放原始碼軟體專案，讓應用程式部署在軟體貨櫃下的工作可以自動化進行", 
	    "Dockers是有能力打包應用程式及其虛擬容器，可以在任何Linux伺服器上執行的依賴性工具", 
		"Docker利用Linux核心中的資源分離機制，例如cgroups，以及Linux核心命名空間（namespaces），來建立獨立的容器（containers）"); 

//定義行動網頁移動:往前一格

	 function prev(){
	    i--; 
	    //當i變成負的,就令i=2
	    //i=2-->1-->0-->-1(負的)令i==2-->1-->0
	    if (i < 0) {i = 2;}
	    //使用jquery的語法
	    $("#roleimg").attr("src", img[i]);		
		$("#rolemsg").text(msg[i]);
      }
//定義行動網頁移動:往後一格
//使用jquery的語法
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
//小測驗:: data-position="fixed"
      <div data-role="header" data-position="fixed">  
 	    <h1>T-shirt 王Docker</h1>
      </div>
      <div data-role="content">	    
		<img src="piece.jpg" width="100%"> 
	    <a href="#story" data-rel="dialog" data-role="button" data-icon="arrow-r">Docker介紹</a>
		<a href="#role" data-role="button" data-icon="arrow-r">Docker功能介紹</a>
		<a href="https://www.docker.com/" data-rel="external" data-role="button" data-icon="arrow-r">Docker官方網站</a>
	  </div>
//表尾===使用data-role="footer"  
      <div data-role="footer" data-position="fixed">
	    <h4>&copy;快樂學Docker</h4>
	  </div>
    </div>
    
    
 //定義story	
	<div data-role="page" id="story">
	  <div data-role="header">
	    <h1>Docker介紹</h1>	            
      </div>
      <div data-role="content">
        <p>Docker是一個開放原始碼軟體專案，讓應用程式部署在軟體貨櫃下的工作可以自動化進行，藉此在Linux作業系統上，
		提供一個額外的軟體抽象層，以及作業系統層虛擬化的自動管理機制[1]。

Docker利用Linux核心中的資源分離機制，例如cgroups，以及Linux核心命名空間（namespaces），來建立獨立的容器（containers）。這可以在單一Linux實體下運作，避免啟動一個虛擬機器造成的額外負擔[2]。Linux核心對命名空間的支援完全隔離了工作環境中應用程式的視野，包括行程樹、網路、用戶ID與掛載檔案系統，而核心的cgroup提供資源隔離，包括CPU、記憶體、block I/O與網路。從0.9版本起，Dockers在使用抽象虛擬是經由libvirt的LXC與systemd - nspawn提供介面的基礎上，開始包括libcontainer函式庫做為以自己的方式開始直接使用由Linux核心提供的虛擬化的設施，

依據行業分析公司「451研究」：「Dockers是有能力打包應用程式及其虛擬容器，可以在任何Linux伺服器上執行的依賴性工具，這有助於實現靈活性和可攜式性，應用程式在任何地方都可以執行，無論是公有雲、私有雲、單機等。</p>
      </div>
	</div>


//定義role
	<div data-role="page" id="role">
	  <div data-role="header">
	    <h1>Docker介紹</h1>	            
      </div>
	  <div data-role="content">
	    <img id="roleimg" src="piece1.jpg" width="100%">
		<p id="rolemsg">Docker利用Linux核心中的資源分離機制。</p>
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

## My ex

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
	<title>R語言的行動網站</title>
	<link rel="stylesheet" href="http://code.jquery.com/mobile/1.4.5/jquery.mobile-1.4.5.min.css" />
    <script src="http://code.jquery.com/jquery-2.2.3.min.js"></script>
    <script src="http://code.jquery.com/mobile/1.4.5/jquery.mobile-1.4.5.min.js"></script>    
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<script>
	  var i = 0;
      var img = new Array("a.jpg", "b.jpg", "c.jpg");
      var msg = new Array("人生苦短，我用python", "Github", "Docker"); 
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
    <div data-role="page" id="home">
      <div data-role="header" data-position="fixed">  
 	    <h1>R語言的行動網站</h1>
      </div>
        
      <div data-role="content">	    
		<img src="e.png" width="80%" height="90%"> 
	    <a href="#story" data-rel="dialog" data-role="button" data-icon="arrow-r">R語言介紹</a>
		<a href="#role" data-role="button" data-icon="arrow-r">角色介紹</a>
		<a href="https://www.r-project.org/" data-rel="external" data-role="button" data-icon="arrow-r">R語言官方網站</a>
        <a href="https://blog.gtwang.org/r/introduction-to-r-language/" data-rel="dialog" data-role="button" data-icon="arrow-r">大數據時代中求生存</a>
	  </div>	  

      <div data-role="footer" data-position="fixed">
	    <h4>&copy;快樂學R語言</h4>
	  </div>
    </div>
 

     <div data-role="page" id="story">
	  <div data-role="header">
	    <h1>R語言介紹</h1>	            
      </div>
      <div data-role="content">
      <p>一、R 是什麼？R 這個名稱其實代表兩個東西，一個是 R 這個程式語言，另外一個是執行 R 程式的軟體環境，所以 R 這個字同時是程式語言以及軟體的名稱，而當我們在書籍或是網路上看到 R 這個名詞時，通常應該都很容易辨別它是代表哪一種（甚至同時意指這兩種）。
      二、R 程式語言R 程式語言誕生於 90 年代初期，由奧克蘭大學的 Ross Ihaka 與 Robert Gentleman 所發展出來的，它是以 S 語言（誕生於 70 年代的貝爾實驗室，主要作者為 John Chambers）為基礎所發展出來的一個 GNU 專案，以免費且開放的方式釋出其原始碼，目前 R 這個專案是由 R Core Team 的二十位成員負責開發與維護。由於 R 語言（S 語言）從 70 年代持續演變至今，經過了好幾個世代，並不像近代的新興程式語言（如微軟的 .Net）是全新設計的，所以 R 的語法在某些時候會讓人感覺很奇怪，或是同時允許好幾種不同的寫法，這個現象是一個語言經過長期自由發展之後所難以避免的。當然語言很自由也是有優點的，如果您不喜歡 R 原本的功能，我們可以自己動手直接改寫我們想要的功能，而且通常我們要的功能都已經有人寫好了，我們的問題通常不是「R 可以處理這個問題嗎？」，反而我們會問「這裡有三種實作版本，我應該用哪一個？」。
      三、R 語言本身是屬於高階的直譯式語言（interpreted language），所以在程式執行之前，使用者不需要自己編譯程式，我們可以把心力全部投入在資料的分析上，不用去管太低階的電腦問題，就跟使用 Matlab 這類的程式語言類似。
      四、R 本身支援混合式的程式設計模式，在他的內部核心中是以指令式程式設計（imperative programming）來撰寫的（就像一般的指令稿，一行接著一行執行），但它也支援物件導向程式設計（object-oriented programming）與函數式程式設計（functional programming），混合式的程式設計風格會讓一個問題有好幾種解決方式，程式設計師可以依自己的喜好來選擇。</p>
      </div>
	</div>
	
	<div data-role="page" id="role">
	  <div data-role="header">
	    <h1>人物介紹</h1>	            
      </div>

	  <div data-role="content">
	    <img id="roleimg" src="e.png" width="100%">
		<p id="rolemsg">免費：R 是以開放原始碼的授權釋出的，完全免費。
                        開放：R 是 S 語言的開放原始碼實做版本，您可以將 S-plus 的程式碼直接放進 R 中執行。
                        佔有率高：SAS 是最普遍被使用的統計軟體，但在學術界最普及的統計軟體是 R 與 S 語言，尤其在統計的期刊中，常常可以看到 R 語言的蹤跡。
                        跨平台：R 可以在各種平台上運作，包含 Windows、Macintosh、Linux 等數十種平台。
                        彈性大：R 是一種程式語言，使用者可以自行撰寫適合自己的分析程式。
                        互動式：傳統的統計分析軟體，是將所有的統計分析過程一次做完，產生報表，而 R 可以互動式的一步一步處理，使用者可以依照每一步的結果而決定下一步該如何處理。</p>
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
