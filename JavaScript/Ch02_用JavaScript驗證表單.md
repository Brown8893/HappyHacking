# Ch02_用JavaScript驗證表單

## 2.1 最簡單的表單驗證—禁止空白的必填項目
### 2.1.1 最簡單表單的HTML結構
>* 【Ex2-1 最簡單表單的HTML結構】
```
<!DOCTYPE html>
<html>
 <head>
  <title>最簡單表單的HTML結構</title>
 </head>
 <body>
	<form method="post" action="">
		帳戶：<input type="text" name="" /><br /><br />
		密碼：<input type="password" name="" /><br /><br />
		確認：<input type="password" name="" /><br /><br />
		<input type="submit" value="註冊"/>
	</form>
 </body>
</html>
```
### 2.1.2 綁定驗證功能
>* 【Ex2-2 註冊事件】
```
<!DOCTYPE html>
<html>
 <head>
  <title>註冊事件</title>
 </head>
 <body>
	<form method="post" action="">
		帳戶：<input type="text" name="" id="userid" /><br /><br />
		密碼：<input type="password" name="" id="userpwd" /><br /><br />
		確認：<input type="password" name="" id="userpwd2" /><br /><br />
		<input type="submit" value="註冊" onclick="return eg.regCheck();" />
	</form>
	<script>
	var eg = {};//聲明一個對象，當作命名空間來使用，本書默認的範例都會以此來管理
		eg.regCheck = function(){

		}
	</script>
 </body>
</html>
```
>* 【Ex2-3 給表單添加驗證功能】
```
<!DOCTYPE html>
<html>
 <head>
  <title>給表單添加驗證功能</title>
 </head>
 <body>
	<form method="post" action="">
		帳戶：<input type="text" name="" id="userid" /><br /><br />
		密碼：<input type="password" name="" id="userpwd" /><br /><br />
		確認：<input type="password" name="" id="userpwd2" /><br /><br />
		<input type="submit" value="註冊" onclick="return eg.regCheck();" />
	</form>
	<script>
		var eg = {};//聲明一個對象，當作命名空間來使用，本書默認的範例都會以此來管理
			//定義一個公共函數來獲取指定id元素的值，減少代碼量，提高代碼復用率
			eg.$ = function(id){
				return document.getElementById(id);
			};
			eg.regCheck = function(){
				var uid = eg.$("userid");
				var upwd = eg.$("userpwd");
				var upwd2 = eg.$("userpwd2");
				if(uid.value == ''){
					alert('帳戶不能為空!');
					return false;
				}
				if(upwd.value == ''){
					alert('密碼不能為空!');
					return false;
				}
				if(upwd.value != upwd2.value){
					alert('兩次密碼輸入不相同!');
					return false;
				}
				return true;
			};
	</script>
 </body>
</html>
```
### 2.1.3 綁定驗證的另外一種方式
>* 【Ex2-4 form表單綁定驗證完整範例】
```
<!DOCTYPE html>
<html>
 <head>
  <title>form表單綁定驗證完整範例</title>
 </head>
 <body>
	<form method="post" action="" onsubmit="return eg.regCheck();">
		帳戶：<input type="text" name="" id="userid" /><br /><br />
		密碼：<input type="password" name="" id="userpwd" /><br /><br />
		確認：<input type="password" name="" id="userpwd2" /><br /><br />
		<input type="submit" value="註冊" />
	</form>
	<script>
		var eg = {};//聲明一個對象，當作命名空間來使用，本書默認的範例都會以此來管理
			//定義一個公共函數來獲取指定id元素的值，減少代碼量，提高代碼復用率
			eg.$ = function(id){
				return document.getElementById(id);
			};
			eg.regCheck = function(){
				var uid = eg.$("userid");
				var upwd = eg.$("userpwd");
				var upwd2 = eg.$("userpwd2");
				if(uid.value == ''){
					alert('帳戶不能為空!');
					return false;
				}
				if(upwd.value == ''){
					alert('密碼不能為空!');
					return false;
				}
				if(upwd.value != upwd2.value){
					alert('兩次密碼輸入不相同!');
					return false;
				}
				return true;
			};
	</script>
 </body>
</html>
```
## 2.2 處理各種的表單元素
### 2.2.1 input,textarea,hidden和butten
>* 【Ex2-5 處理各種類型的表單(一)】
```
<!DOCTYPE html>
<html>
 <head>
  <title>處理各種類型的表單(一)</title>
 </head>
 <body>
	<form method="post" action="" onsubmit="return eg.regCheck();">
		<input type="hidden" name="" id="errnum" value="0"/>
		帳戶：<input type="text" name="" id="userid" /><br /><br />
		密碼：<input type="password" name="" id="userpwd" /><br /><br />
		確認：<input type="password" name="" id="userpwd2" /><br /><br />
		簡介：<textarea name="" rows="4" cols="18" id="about"></textarea> <br /><br />
		<input type="submit" value="注册" id="regBtn" /> <input type="button" value="解锁" onclick="eg.unlock()" style="display:none;" id="regUnlock" />
	</form>
	<script>
		var eg = {};//聲明一個對象，當作命名空間來使用，本書默認的範例都會以此來管理
			//定義一個公共函數來獲取指定id元素的值，減少代碼量，提高代碼復用率
			eg.$ = function(id){
				return document.getElementById(id);
			};
			//主要的驗證方法
			eg.regCheck = function(){
				var uid = eg.$("userid");
				var upwd = eg.$("userpwd");
				var upwd2 = eg.$("userpwd2");
				if(uid.value == ''){
					alert('帳戶不能為空!');
					eg.err();
					return false;
				}
				if(upwd.value == ''){
					alert('密碼不能為空!');
					eg.err();
					return false;
				}
				if(upwd.value != upwd2.value){
					alert('兩次密碼輸入不相同!');
					eg.err();
					return false;
				}
				//新增的部分
				var about = eg.$("about");
				if(about.value.length>60){
					alert('簡介太長!');
					eg.err();
					return false;
				}
				return true;
			};
			//出錯時記錄錯誤次數。
			eg.err = function(){
				var el = eg.$("errnum");
				var old = el.value;
				el.value = parseInt(old)+1;//把字符串轉換為整数+1，並保存起来
				eg.lock();//用來檢查是否應該鎖定。
			};
			//通過次數判斷是否要鎖定註冊
			eg.lock = function(){
				var err = eg.$("errnum");
				if(parseInt(err.value)>2){
					eg.$("regBtn").disabled = true;//根據服務需求，錯誤3次就鎖定
					eg.$("regUnlock").style.display="block";//同時顯示解鎖按鈕
				}
			};
			//解鎖
			eg.unlock = function(){
				eg.$("regBtn").disabled = false;//根據業務需求，解鎖就是讓用戶可以重新註冊
				eg.$("regUnlock").style.display="none";
			}
	</script>
 </body>
</html>
```
### 2.2.2 checkbox,radio,和select
>* 【Ex2-6 處理各種類型的表單(二)】
```
<!DOCTYPE html>
<html>
 <head>
  <title>處理各種類型的表單(二)</title>
 </head>
 <body>
	<form method="POST" onSubmit="return eg.regCheck();">
		<input type="hidden" name="" id="errnum" value="0"/>
		帳戶：<input type="text" name="" id="userid" /><br /><br />
		密碼：<input type="password" name="" id="userpwd" /><br /><br />
		確認：<input type="password" name="" id="userpwd2" /><br /><br />
		性别：<input type="radio" name="sex" value="1" checked="checked" />男 <input type="radio" name="sex" value="0"/>女 <br /><br />
		年齡：<select name="" id="age">
			<option value="0"  selected="selected">請選擇年齡段</option>
			<option value="1">18歲以下</option>
			<option value="2">18-24歲</option>
			<option value="3">24-30歲</option>
			<option value="4">20-35歲</option>
			<option value="5">35歲以上</option>
		</select><br /><br />
		愛好：<input type="checkbox" name="like" value="1" class="like"/>上網 <input type="checkbox" name="like" value="2" class="like"/>逛街  <input type="checkbox" name="like" value="3" class="like"/>看電影  <input type="checkbox" name="like" value="4" class="like"/>其他 <br /><br />
		簡介：<textarea name="" rows="4" cols="18" id="about"></textarea> <br /><br />
		<input type="submit" value="注册" id="regBtn" /> <input type="button" value="解锁" onclick="eg.unlock()" style="display:none;" id="regUnlock" />
	</form>
	<script>
		var eg = {};//聲明一個對象，當作命名空間來使用，本書默認的範例都會以此來管理
			//定義一個公共函數來獲取指定id元素的值，減少代碼量，提高代碼復用率
			eg.$ = function(id){
				return document.getElementById(id);
			};
			//主要的驗證方法
			eg.regCheck = function(){
				var uid = eg.$("userid");
				var upwd = eg.$("userpwd");
				var upwd2 = eg.$("userpwd2");
				if(uid.value == ''){
					alert('帳戶不能為空!');
					eg.err();
					return false;
				}
				if(upwd.value == ''){
					alert('密碼不能為空!');
					eg.err();
					return false;
				}
				if(upwd.value != upwd2.value){
					alert('兩次密碼輸入不相同!');
					eg.err();
					return false;
				}
				//新增的部分
				var about = eg.$("about");
				if(about.value.length>60){
					alert('簡介太長!');
					eg.err();
					return false;
				}
				//2次新增
				var age = eg.$("age");
				if(age.value == "0"){
					alert('請選擇年齡段!');
					eg.err();
					return false;
				}
				
				var likes = document.getElementsByClassName("like");
				var likeNum = 0;
					for(var n=0;n<likes.length;n++){
						if(likes[n].checked){
							likeNum++;
						}
					}
				if(likeNum==0){
					alert('請至少選擇一個愛好!');
					eg.err();
					return false;
				}
				return true;
			};
			//出錯時記錄錯誤次數。
			eg.err = function(){
				var el = eg.$("errnum");
				var old = el.value;
				el.value = parseInt(old)+1;//把字符串轉換為整数+1，並保存起来
				eg.lock();//用來檢查是否應該鎖定。
			};
			//通過次數判斷是否要鎖定註冊
			eg.lock = function(){
				var err = eg.$("errnum");
				if(parseInt(err.value)>2){
					eg.$("regBtn").disabled = true;//根據服務需求，錯誤3次就鎖定
					eg.$("regUnlock").style.display="block";//同時顯示解鎖按鈕
				}
			};
			//解鎖
			eg.unlock = function(){
				eg.$("regBtn").disabled = false;//根據業務需求，解鎖就是讓用戶可以重新註冊
				eg.$("regUnlock").style.display="none";
			}
	</script>
 </body>
</html>
```
>* 【Ex2-7 兼容各瀏覽器的獲取指定class名稱元素集合的方法】
```
<!DOCTYPE html>
<html>
 <head>
  <title>相容各瀏覽器的獲取指定class名稱元素集合的方法</title>
 </head>
 <body>
	<form method="POST" onSubmit="return eg.regCheck();">
		<input type="hidden" name="" id="errnum" value="0"/>
		帳戶：<input type="text" name="" id="userid" /><br /><br />
		密碼：<input type="password" name="" id="userpwd" /><br /><br />
		確認：<input type="password" name="" id="userpwd2" /><br /><br />
		性別：<input type="radio" name="sex" value="1" checked="checked" />男 <input type="radio" name="sex" value="0"/>女 <br /><br />
		年齡：<select name="" id="age">
			<option value="0"  selected="selected">請選擇年齡段</option>
			<option value="1">18歲以下</option>
			<option value="2">18-24歲</option>
			<option value="3">24-30歲</option>
			<option value="4">20-35歲</option>
			<option value="5">35歲以上</option>
		</select><br /><br />
		愛好：<input type="checkbox" name="like" value="1" class="like"/>上網 <input type="checkbox" name="like" value="2" class="like"/>逛街  <input type="checkbox" name="like" value="3" class="like"/>看電影  <input type="checkbox" name="like" value="4" class="like"/>其他 <br /><br />
		簡介：<textarea name="" rows="4" cols="18" id="about"></textarea> <br /><br />
		<input type="submit" value="註冊" id="regBtn" /> <input type="button" value="解鎖" onclick="eg.unlock()" style="display:none;" id="regUnlock" />
	</form>
	<script>
		var eg = {};//聲明一個物件，當做命名空間來使用，本書預設的範例都會以此來方便管理
			//定義一個公共函數來獲取指定id元素，減少代碼量，提高代碼複用率
			eg.$ = function(id){
				return document.getElementById(id);
			};
			//定義一個公共函數來獲取指定class名稱的元素集合，能相容各流覽器
			eg.getElementsByClassName = function(className, element) {
				if(document.getElementsByClassName){
					return (element || document).getElementsByClassName(className)
				}
				var children = (element || document).getElementsByTagName('*');
				var elements = new Array();
			 
				for (var i = 0; i < children.length; i++) {
					var child = children[i];
					var classNames = child.className.split(' ');
					for (var j = 0; j < classNames.length; j++) {
						if (classNames[j] == className) {
							elements.push(child);
							break;
						}
					}
				}
				return elements;
			};
			//主要的驗證方法
			eg.regCheck = function(){
				var uid = eg.$("userid");
				var upwd = eg.$("userpwd");
				var upwd2 = eg.$("userpwd2");
				if(uid.value == ''){
					alert('帳戶不能為空!');
					eg.err();
					return false;
				}
				if(upwd.value == ''){
					alert('密碼不能為空!');
					eg.err();
					return false;
				}
				if(upwd.value != upwd2.value){
					alert('兩次密碼輸入不相同!');
					eg.err();
					return false;
				}
				//新增的部分
				var about = eg.$("about");
				if(about.value.length>60){
					alert('簡介太長!');
					eg.err();
					return false;
				}
				//2次新增
				var age = eg.$("age");
				if(age.value == "0"){
					alert('請選擇年齡段!');
					eg.err();
					return false;
				}
				
				var likes = eg.getElementsByClassName("like");
				var likeNum = 0;
					for(var n=0;n<likes.length;n++){
						if(likes[n].checked){
							likeNum++;
						}
					}
				if(likeNum==0){
					alert('請至少選擇一個愛好!');
					eg.err();
					return false;
				}
				return true;
			};
			//出錯時記錄錯誤次數。
			eg.err = function(){
				var el = eg.$("errnum");
				var old = el.value;
				el.value = parseInt(old)+1;//把字串轉換為整數+1，並保存起來
				eg.lock();//用來檢查是否應該鎖定。
			};
			//通過次數判斷是否要鎖定註冊
			eg.lock = function(){
				var err = eg.$("errnum");
				if(parseInt(err.value)>2){
					eg.$("regBtn").disabled = true;//根據業務需求，輸錯3次就鎖定
					eg.$("regUnlock").style.display="block";//同時顯示解鎖按鈕
				}
			};
			//解鎖
			eg.unlock = function(){
				eg.$("regBtn").disabled = false;//根據業務需求，解鎖就是讓用戶可以重新註冊
				eg.$("regUnlock").style.display="none";
			}
	</script>
 </body>
</html>
```
## 2.3 用正則來校驗複雜的格式要求
### 2.3.1 認識JavaScript正則：正則表示法
### 2.3.2 JavaScript正則符號及其說明
```
\ 將下一個字元標記為一個特殊字元、原義字元、向後引用或八進制轉換字元
^ 匹配輸入字串的開始位置
$ 匹配輸入字串的結束位置
* 匹配前面的子表達式零次或多次
+ 匹配前面的子表達式一次或多次
? 匹配前面的子表達式零次或一次
? 當該字元緊跟在任何一個其他限制字元後面時，匹配模式為非貪婪
{n} n是一個非整負整數。匹配確定的n次
{n,} n是一個非整負整數。至少匹配n次
{n,m} m和n均為非負整數。其中n<=m
. 匹配除"\n"之外的任何單個字元
(pattern) 匹配pattern並獲取這一匹配
(?:pattern) 匹配pattern但不獲取結果(意即非獲取匹配，不進行儲存)
(?=pattern) 正向預查，在任何匹配pattern的字串開始處匹配找查字串(意即非獲取匹配，不需獲取以供使用)
(?！pattern) 負向預查，在任何不匹配pattern的字串開始處匹配找查字串(意即非獲取匹配，不需獲取以供使用)
x|y 匹配x或y
[xyz] 字元集合
[^xyz] 負值字元集合
[a-z] 字元範圍
[^a-z] 負值字元範圍
\b 匹配一個單字邊界
\B 匹配非單字邊界
\cx 匹配由x指明的控制字元
\d 匹配一個數字字元=[0-9]
\D 匹配一個非數字字元=[^0-9]
\f 匹配一個換頁符=\x0c、\cL
\n 
\r
\s
\S
\t
\v
\w
\W
\xn
\num
\n
\nm
\nml
\un
```
### 2.3.3 正則驗證輸入信箱
## 2.4 改善用戶體驗
### 2.4.1 甚麼是用戶體驗
### 2.4.2 表單的用戶體驗改善
>* 【Ex2-8 改善表單的用戶驗證】
```
<!DOCTYPE html>
<html>
 <head>
  <title>改善用戶體驗的表單</title>
  <style>
  #pwdLvSpan{display:inline-block;width:100px;height:5px;background:#c3c3c3;}
  #pwdLvSpan i{display:block;background:green;height:5px;width:0;}
  </style>
 </head>
 <body>
	<form method="POST" onSubmit="return eg.regCheck();">
		<input type="hidden" name="" id="errnum" value="0"/>
		帳戶：<input type="text" name="" id="userid" /><br /><br />
		密碼：<input type="password" name="" id="userpwd" /> 密碼強度 <span id="pwdLvSpan"><i id="pwdLv"></i></span><br /><br />
		確認：<input type="password" name="" id="userpwd2" /><br /><br />
		性別：<input type="radio" name="sex" value="1" checked="checked" />男 <input type="radio" name="sex" value="0"/>女 <br /><br />
		年齡：<select name="" id="age">
			<option value="0"  selected="selected">請選擇年齡段</option>
			<option value="1">18歲以下</option>
			<option value="2">18-24歲</option>
			<option value="3">24-30歲</option>
			<option value="4">20-35歲</option>
			<option value="5">35歲以上</option>
		</select><br /><br />
		愛好：<input type="checkbox" name="like" value="1" class="like"/>上網 <input type="checkbox" name="like" value="2" class="like"/>逛街  <input type="checkbox" name="like" value="3" class="like"/>看電影  <input type="checkbox" name="like" value="4" class="like"/>其他 <br /><br />
		簡介：<textarea name="" rows="4" cols="18" id="about"></textarea> <br /><br />
		郵箱：<input type="text" name="" id="email" /><br /><br />
		<input type="submit" value="註冊" id="regBtn" /> <input type="button" value="解鎖" onclick="eg.unlock()" style="display:none;" id="regUnlock" />
	</form>
	<script>
		var eg = {};//聲明一個物件，當做命名空間來使用，本書預設的範例都會以此來方便管理
			//定義一個公共函數來獲取指定id元素，減少代碼量，提高代碼複用率
			eg.$ = function(id){
				return document.getElementById(id);
			};
			//定義一個公共函數來獲取指定class名稱的元素集合，能相容各流覽器
			eg.getElementsByClassName = function(className, element) {
				if(document.getElementsByClassName){
					return (element || document).getElementsByClassName(className)
				}
				var children = (element || document).getElementsByTagName('*');
				var elements = new Array();
			 
				for (var i = 0; i < children.length; i++) {
					var child = children[i];
					var classNames = child.className.split(' ');
					for (var j = 0; j < classNames.length; j++) {
						if (classNames[j] == className) {
							elements.push(child);
							break;
						}
					}
				}
				return elements;
			};
			//定義一個公共函數來解決事件監聽的相容問題
			eg.addListener = function(target,type,handler){
				if(target.addEventListener){
					target.addEventListener(type,handler,false);
				}else if(target.attachEvent){
					target.attachEvent("on"+type,handler);
				}else{
					target["on"+type]=handler;
				}
			};
			//主要的驗證方法
			eg.regCheck = function(){
				var uid = eg.$("userid");
				var upwd = eg.$("userpwd");
				var upwd2 = eg.$("userpwd2");
				if(uid.value == ''){
					alert('帳戶不能為空!');
					uid.focus();
					eg.err();
					return false;
				}
				if(upwd.value == ''){
					alert('密碼不能為空!');
					upwd.focus();
					eg.err();
					return false;
				}
				if(upwd.value != upwd2.value){
					alert('兩次密碼輸入不相同!');
					upwd.focus();
					eg.err();
					return false;
				}
				//新增的部分
				var about = eg.$("about");
				if(about.value.length>60){
					alert('簡介太長!');
					about.focus();
					eg.err();
					return false;
				}
				//2次新增
				var age = eg.$("age");
				if(age.value == "0"){
					alert('請選擇年齡段!');
					age.focus();
					eg.err();
					return false;
				}
				
				var likes = eg.getElementsByClassName("like");
				var likeNum = 0;
					for(var n=0;n<likes.length;n++){
						console.log(likes[n].checked)
						if(likes[n].checked){
							likeNum++;
						}
					}
				if(likeNum==0){
					alert('請至少選擇一個愛好!');
					eg.err();
					return false;
				}
				//郵箱驗證
				var email =  eg.$("email");
				//if(!new RegExp("^[a-z\\d]+[\\w\\-\.]*@([a-z\\d]+[a-z\\d\\-]*\.)+[a-z]{2,4}$","i").test(email.value)){
				if(!/^[A-Za-z\d]+[A-Za-z\d\-_\.]*@([A-Za-z\d]+[A-Za-z\d\-]*\.)+[A-Za-z]{2,4}$/.test(email.value)){
					alert('請輸入正確的郵箱!');
					email.focus();
					eg.err();
					return false;
				}
				return true;
			};
			//添加一些交互事件
			eg.addEvent = function(){
				var pwd = eg.$("userpwd");
				eg.addListener(pwd,"keyup",function(){
					var lv=0;
					if(/^\d{4,}$/.test(pwd.value)){
						lv = 10;
					}else if(/^\w{4,}$/.test(pwd.value)){
						lv = 25;
					}else if (/^[\d\w]{4,}$/.test(pwd.value)){
						lv = 50;
					}else if (/^[\d\w~!@#$%\^&*\(\)\-{}\[\]=<>,\.\?\/]{4,}$/.test(pwd.value)){
						lv = 100;
					}else if(pwd.value.length<6 && pwd.value.length>3){
						lv = 60;
					}else if(pwd.value.length<4){
						lv = 0;
					}
					eg.$("pwdLv").style.width = lv+"px";
				});
			}
			//在使用者按一下註冊按鈕前就要運行起來,所以定義好就立刻調用
			eg.addEvent();
			//出錯時記錄錯誤次數。
			eg.err = function(){
				var el = eg.$("errnum");
				var old = el.value;
				el.value = parseInt(old)+1;//把字串轉換為整數+1，並保存起來
				eg.lock();//用來檢查是否應該鎖定。
			};
			//通過次數判斷是否要鎖定註冊
			eg.lock = function(){
				var err = eg.$("errnum");
				if(parseInt(err.value)>2){
					eg.$("regBtn").disabled = true;//根據業務需求，輸錯3次就鎖定
					eg.$("regUnlock").style.display="block";//同時顯示解鎖按鈕
				}
			};
			//解鎖
			eg.unlock = function(){
				eg.$("regBtn").disabled = false;//根據業務需求，解鎖就是讓用戶可以重新註冊
				eg.$("regUnlock").style.display="none";
			}
	</script>
 </body>
</html>
```
