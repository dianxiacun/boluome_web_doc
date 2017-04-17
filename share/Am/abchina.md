### 关于和农行对接分享
####  一.对客户即农行APP的简单描述
##### 1. 客户的APP的webview是撑屏的，即没有导航栏，也就是显示时间充电的部分约为20px
     
```javascript
//对农行的特别处理，关于判断IOS的顶部20px问题
var ua = navigator.userAgent.toLowerCase();
var android = window.android;
var iOS = window.iOS;
var titleheight = 45;
if(/android/.test(ua)) {
    //如果是安卓的话执行的事件
    var padTop = 0 ;
} else if(/iphone|ipad|ipod/.test(ua)) {
    //如果是IOS需要执行的事件
    var padTop = 20 * (document.documentElement.clientWidth / 320);
} 
//在执行特别处理
$('body').css('paddingTop',padTop+'px');
```
##### 2. 在农行的项目中，我们需要自己加入返回按钮，即html的页面之间的跳转由我们控制，但是首页的返回按钮调用的是他们的方法(放在全局即可)
```javascript
//农行安卓物理返回特别处理----
function back(){
	window.location.href = escape('https://web2native|channel=goto_xhtml*path=login/xhtml/unlogin_menu_location.xhtml');
}
function setAndroidBackKey(backKeyFunc){
    var onBackKey = backKeyFunc;
    function connectWebViewJavascriptBridge(callback){
     if (window.WebViewJavascriptBridge) { 
      callback(WebViewJavascriptBridge);
     } else { 
      document.addEventListener('WebViewJavascriptBridgeReady' , function() {
       callback(WebViewJavascriptBridge) 
      },false);
     }
}
function onBackPressed() {
WebViewJavascriptBridge.callHandler('setPhysicalBackListener', {}, function(responseData) {
	onBackPressed();
     });
onBackKey();
}
connectWebViewJavascriptBridge(function(bridge) { bridge.init(function(message, responseCallback) {});
bridge.callHandler('setPhysicalBackListener', {}, function(responseData) {
	  onBackPressed();
	});
});
}

window.onload = setAndroidBackKey(back)
```
##### 3. 农行的用户绑定，农行的用户绑定除了平常的customerUserId，userPhone, token 之外还有特殊的值 ，所以如果进首页用户绑定失败的话记得做处理，还有一点需要特别注意，就是农行收也是需要订单列表页，当支付的时候通常会跳转到第三方支付平台，为了防止用户信息丢失，用户绑定成功暂时解决方法是session，local都存一份，订单列表页面取用

##### 4. 农行的APP是会传经纬度的
```javascript
//longitude   经度
//latitude    纬度
```
