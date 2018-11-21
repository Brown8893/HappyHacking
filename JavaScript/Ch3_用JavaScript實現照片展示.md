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
>* 【Ex3-3 】
