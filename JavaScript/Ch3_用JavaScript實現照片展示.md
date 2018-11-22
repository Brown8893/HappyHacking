# Ch3_用JavaScript實現照片展示
>* 【Ex3-1 照片展示的HTML代碼】
```
<!DOCTYPE html>
<html>
 <head>
   <title>照片展示</title>
   <link rel="stylesheet" href="eg3.css" type="text/css" />
 </head>
 <body>
 <div  id="bigPhoto"><img  id="bigPhotoSrc"  src="photo01.jpg" width="620" height="450" border="0" alt=""></div>
 <div id="smallPhotos">
   <span id="prve"></span>
   <ul id="smallPhotoList"></ul>
   <span id="next"></span>
 </div>
 <script src="eg3.js"></script>
 </body>
</html>
```
>* 【Ex3-2 照片展示的CSS代碼】
```
  ul,li{
         list-style: none;
	   }
#smallPhotos{width:620px; margin: 10px 0;}
#smallPhotoList{margin: 0 auto; width:580px; float:left;padding: 0;}
#smallPhotoList li{
       float:left;            //左浮動
	   margin-left: 10px;     //左外邊距10像素
	   _margin-left:8px;      //這是專門針對IE6間隙太大而設置的
}
#smallPhotoList img{
       border:2px solid #000;
	   cursor:pointer;
}
#prve{
        background: url(icon_prve.jpg);
		height: 40px;
		width:20px;
		display: inline-block;
		float: left;
		cursor:pointer;
}
#next{
        background: url(icon_next.jpg);
		height:40px;
		width:20px;
		display: inline-block;
		float: right;
		cursor:pointer;
}
```
>* 【Ex3-3 照片顯示的JavaScript代碼】
```
eg.data = [
       ["photo01.jpg","thumb01.jpg"]
	   ,["photo02.jpg","thumb02.jpg"]
	   ,["photo03.jpg","thumb03.jpg"]
	   ,["photo04.jpg","thumb04.jpg"]
	   ,["photo05.jpg","thumb05.jpg"]
	   ,["photo06.jpg","thumb06.jpg"]
	   ,["photo07.jpg","thumb07.jpg"]
	   ,["photo01.jpg","thumb01.jpg"]
	   ,["photo02.jpg","thumb02.jpg"]
	   ,["photo03.jpg","thumb03.jpg"]
	   ,["photo04.jpg","thumb04.jpg"]
	   ,["photo05.jpg","thumb05.jpg"]
	   ,["photo06.jpg","thumb06.jpg"]
	   ,["photo07.jpg","thumb07.jpg"]
];
eg.shoeNumber = 0;                                  //默認顯示
eg.groupNumber = 1;                                 //當前顯示的組
eg.groupSize = 6;                                   //每組的數量
eg.showThumb = function(group){             
       var ul = eg.$("smallPhotosList");
	   ul.innerHTML = '';                       //每次顯示時要清空舊的內容
	   var start = (group-1)*eg.groupSize;      //計算需要的data數據的開始位置
	   var end = group*eg.groupSize             //計算需要的end數據的開始位置
	   for(var i=start;(i<end&&i<eg.data.length);i++){
	          //循環數據，並根據數據生成HTML後插入小圈列表裡
			  var li = document.createElement("li");
			  il.innerHTML = '<img src="'+eg.data[i][l]+'" id="thumb'+ i+'"width="80" height="40"/>';
			  ul.appendChild(li);        //追加元素
	   }
};
eg.init = function(){
       eg.showThumb(1);                             //初始化要顯示的
};
eg.init();
```
>* 【Ex3-4 響應小照片單擊動作】
```

```
