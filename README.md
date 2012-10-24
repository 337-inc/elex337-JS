# ELEX337 JS SDK #

## 加载与初始化 ##

通过以下代码可以加载Elex337 JS SDK ，并初始化。请把其中的 YOUR_APP_ID 与 WWW.YOUR_DOMAIN.COM 替换成我们提供的 appid 与您的域名。这段代码应该紧跟在<body>标签之后
	```
	<div id="elex337-root"></div>
	<script>
	  window.Elex337AsyncInit = function() {
	    // init the Elex337 JS SDK
	    Elex337.init({
	      appId      : 'YOUR_APP_ID', // App ID 
	      channelUrl : '//WWW.YOUR_DOMAIN.COM/channel.html', // Channel File for x-domain communication
	      status     : true, // check the login status upon init?
	      cookie     : true, // set sessions cookies to allow your server to access the session?
	      header     : true  // auto insert 337 header?
	    });
	
	    // 其余初始化代码
	
	  };
	
	  // 异步加载337js
	  (function(d){
	     var js, id = 'elex337-jssdk', ref = d.getElementsByTagName('script')[0];
	     if (d.getElementById(id)) {return;}
	     js = d.createElement('script'); js.id = id; js.async = true;
	     js.src = "http://337.eleximg.com/337/connect/all.1.0.js";
	     ref.parentNode.insertBefore(js, ref);
	   }(document));
	</script>
	```

### 初始化 ###
以上代码会异步的加载SDK源码，因此不会阻塞你页面中的其他请求。其中Elex337AsyncInit方法会在SDK加载完成之后立即执行。任何你希望在SDK加载完成之后执行的代码都应该放在Elex337AsyncInit方法中执行。

### elex337-root 标签 ###
SDK依赖于此标签，请不要在此标签上添加任何样式


## 部署Channel File ##

在部分浏览器下SDK需要Channel File以便处理跨域的请求。 请将Channel File部署至你的服务器上，内容为：
	```
	<script src="http://337.eleximg.com/337/connect/all.1.0.js"></script>
	```
Channel文件应被尽可能的缓存，以便提高性能。以下为PHP环境下正确设置缓存行为的代码：	
	```
	 <?php
	 $cache_expire = 60*60*24*365;
	 header("Pragma: public");
	 header("Cache-Control: max-age=".$cache_expire);
	 header('Expires: ' . gmdate('D, d M Y H:i:s', time()+$cache_expire) . ' GMT');
	 ?>
	 <script src="http://337.eleximg.com/337/connect/all.1.0.js"></script>
	```
请把Elex337.init中的channelUrl属性指向你部署的channel.html地址。channelUrl虽然是可选项，但是强烈建议提供一份。

## API ##

完成Elex337.init 方法后，就可以使用以下方法了： 

1. 登陆
	Elex337.login(function (result) {
		output(result);
	});
