## 对大屏、电视 （如聚浩大屏、行悦电视）文档总结：
### 一.开发前须知
>#### 1.客户机型(版本)
>#### 2.客户机器的内核及兼容性（浏览器）
>#### 3.客户机型需要适配的尺寸 （如: 1920-1080  1280-720），这里是适配各尺寸的一个案例 : 
- [DEMO](https://github.com/kpboluome/boluome_web_doc/blob/master/share/Am/shipeiDEMO/File/tvDEMO/css.js)
>#### 4.客户机器对性能的适应度
>#### 5.客户与我们对接特别是技术文档，记得抄送一份发给技术人员，以便于文档更新，同时减少不必要的步骤
---------
### 二.开发准备
>#### 1.需求明确
>#### 2.（建议）开发前，如果有关产品的技术人员及时沟通，对此次开发做一定的了解,如果有关于产品的会议尽量参与，使开发人员进一步明确需求
>#### 3.因为机器等不可变因素会影响到成品与最初产品设计有所出入，期间及时商议调整

---------
### 三.开发小提示
>#### 1.     永远不要写死，不然换一个客户或者机器，代码调整过大
>#### 2.     测试DEMO,主要是为了测试这些版本不高，对一些属性或者是动画不兼容，或者性能影响过大而影响流程的机器，在开发前可以用DEMO测试一下，这样在设计以及开发过程中少走弯路
>#### 3.     如果可以的话开发前，可以和客户这方面的技术人员交涉，主要是为了更加详细的了解客户机器，或者他们对自己机器的适配是很有经验的，可以提前了解选择采用，以提高开发效率

---------
### 四.对接说明 (以行悦电视为例子)
>#### 1.物理返回建：
```javascript
 Android.onBackPressed();
 ```
在按返回键的时候对应的方法里面调用
>#### 2.对客户给出的JavaScript 进行全局调用：
```javaScript
function onKeyDown(keyCode){
	if(showMain.isShow == true){
		if(keyCode == 21){
			//要执行的事件...
			console.log('我是左' + keyCode);
		}else if(keyCode == 22){
			//要执行的事件...
			console.log('我是右' + keyCode);
		}else if(keyCode == 19){
			//要执行的事件...
			console.log('我是上' + keyCode);
		}else if(keyCode == 20){
			//要执行的事件...
			console.log('我是下' + keyCode);
		}else if(keyCode == 66){//alert('我是OK');
			//要执行的事件...
			console.log('我是OK' + keyCode);
		}else if(keyCode == 4){
			Android.onBackPressed();
			console.log('我是返回' + keyCode);
		}
	}
	}
```


