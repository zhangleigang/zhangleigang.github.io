title: postMessage
date: 2016-05-16 16:27:01
tags:
---

## [postMessage官方说明](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage)
1. 主要作用：The window.postMessage method safely enables cross-origin communication.
    该方法主要是用来安全的进行跨域通信的。<!-- more -->
2. API调用：
	{% codeblock lang:javascript %}
	otherWindow.postMessage(message, targetOrigin, [transfer]);
	{% endcodeblock %}
	* otherWindow的定义：A reference to another window; such a reference may be obtained, **for example**, using __the contentWindow property of an iframe element__, the object returned by window.open, or by named or numeric index on window.frames.
	我们主要关注的是iframe的window对象，这个通过iframe的contentWindow属性取到值，window.open返回的情况没有试过。
	* targetOrigin 主要用于安全,检验的,一般是发起postMessage方法的域名
3. 代码示例(以主页面和它里面的iframe举例)
     __父页面里面代码__
	{% codeblock lang:javascript %}
	//父页面在http://example.com:8080域名下面
	var iframeWindow = window.frames[0].contentWindow;
    iframeWindow.postMessage("hello there!", "http://example.org");

	function receiveMessage(event)
	{
	  //安全策略
	  if (event.origin !== "http://example.org")
	    return;

	  // event.source is iframeWindow
	  // event.data is "hi there yourself! the secret response is: rheeeeet!"
	}
	window.addEventListener("message", receiveMessage, false);
	{% endcodeblock %}
    
     __iframe页面里面代码__
	{% codeblock lang:javascript %}
	//在postMessage方法被调用后,该方法也会被调用
	//message事件类型其实在postMessage调用后会被触发
	function receiveMessage(event)
	{
	  // Do we trust the sender of this message?
	  if (event.origin !== "http://example.com:8080")
	    return;

	  // event.source is window
	  // event.data is "hello there!"

	  // a convenient idiom for replying to a
	  // message is to call postMessage on event.source and provide
	  // event.origin as the targetOrigin.
	  event.source.postMessage("hi there yourself!  the secret response " +
	                           "is: rheeeeet!",
	                           event.origin);
	}

	window.addEventListener("message", receiveMessage, false);
	{% endcodeblock %}