---
title:  微博授权app过程2
author: hacker
layout: post
permalink:  /weibo-sdk-authorize-app-2/
tags:
  - 移动
  - 授权
---




微博授权app三步走（新浪体育）


上一篇是微盘应用通过微博sdk拿到授权，这个不太一样，不是通过微博sdk来授权的，完全是通过oauth2来操作的。  

<!--more-->

第一步   


	GET https://open.weibo.cn/oauth2/authorize?response_type=code&scope=all&client_id=1104746493&packagename=cn.com.sina.sportslivehd&redirect_uri=http%3A%2F%2F&key_hash=22191242ac93f71da72492a63395bf40&display=mobile HTTP/1.1
	Host: open.weibo.cn
	Proxy-Connection: keep-alive
	Accept-Encoding: gzip, deflate
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
	Accept-Language: zh-cn
	Connection: keep-alive
	User-Agent: Mozilla/5.0 (iPad; CPU OS 7_0_4 like Mac OS X) AppleWebKit/537.51.1 (KHTML, like Gecko) Mobile/11B554a


	HTTP/1.1 200 OK
	Server: nginx/1.2.0
	Date: Wed, 28 May 2014 08:45:33 GMT
	Content-Type: text/html;charset=UTF-8
	Connection: keep-alive
	Pragma: No-cache
	Cache-Control: no-cache
	Expires: Thu, 01 Jan 1970 00:00:00 GMT
	Api-Server-IP: 10.73.89.46
	Vary: Accept-Encoding
	Content-Length: 4126

	<!DOCTYPE html>
	<html>
	<head>
	<meta name="apple-mobile-web-app-capable" content="yes" />
	<meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"/>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
	<title>应用授权 - 新浪体育iPad客户端</title>
	<link href="/oauth2/css/oauthMobileV3/common.css" rel="stylesheet" type="text/css">
	</head>
	<body class="WB_widgets">
	<!--登录前-->
	<div class="container" id="outer">
	<header>
		<img src="/oauth2/images/oauthMobile/logo.png" alt="微博" width="117" height="35">
		 <aside class="logins">
	        <div class="signup_a_container">
	            <a class="signup_a" href="http://weibo.cn/dpool/ttt/h5/reg.php?wm=4406&appsrc=1MjUMl&backurl=https%3A%2F%2Fopen.weibo.cn%2F2%2Foauth2%2Fauthorize%3Fclient_id%3D1104746493%26response_type%3Dcode%26display%3Dmobile%26redirect_uri%3Dhttp%3A%2F%2F%26from%3D%26with_cookie%3D"><em class="signup_a_em">注册</em></a>
		        </div>        
	    </aside>
	    </header>
	<div class="o_body">
	<section>
		<div class="W_login_tit">
		
			授权 新浪体育iPad客户端 访问你的微博帐号
		</div>
	
	<div class="W_btm W_login">
			<form name="authZForm" action="authorize" method="post" node-type="form">
				<input type="hidden" id="display" name="display" value="mobile"/>
			    <input type="hidden" name="action"  id="action" value="login"/>
			    <input type="hidden" name="ticket" id="ticket" value=""/>
			     <input type="hidden" name="scope"  id="scope" value="all"/>
				<input type="hidden" name="isLoginSina"  id="isLoginSina" value=""/>
			    <input type="hidden" name="withOfficalFlag"  id="withOfficalFlag" value="0"/>
			    <input type="hidden" name="quick_auth"  id="quick_auth" value="null"/>
			    <input type="hidden" name="withOfficalAccount"  id="withOfficalAccount" value=""/>
			    <input type="hidden" name="response_type" value="code"/>
			    <input type="hidden" name="regCallback" value="https%3A%2F%2Fopen.weibo.cn%2F2%2Foauth2%2Fauthorize%3Fclient_id%3D1104746493%26response_type%3Dcode%26display%3Dmobile%26redirect_uri%3Dhttp%3A%2F%2F%26from%3D%26with_cookie%3D"/>	
       	        <input type="hidden" name="redirect_uri" value="http://"/>
       	        <input type="hidden" name="client_id" value="1104746493"/>
       	        <input type="hidden" name="appkey62" value="1MjUMl"/>
       	        <input type="hidden" name="state" value=""/>
       	        <input type="hidden" name="from" value=""/>
       	        <input type="hidden" name="offcialMobile" value="true"/>
       	        <input type="hidden" name="verifyToken" value="null"/>
       	        <input type="submit" style="position:absolute; top:-9999px"/>
       	        <div class="login">
			              <input type="email" id="userId" name="userId"  value="请用微博帐号登录" node-type="userid" autocomplete="off" tabindex="1"/>
			              <input type="password"  id="passwd" name="passwd" node-type="passwd" autocomplete="off" tabindex="2"/>
						<div node-type="vdunBox" style="display:none"><input type="text" placeholder="微盾动态码" class="vd" node-type="vdun" maxlength=6 tabindex="3" /></div>
						<div class="code_con" node-type="validateBox" style="display:none"><input type="text" class="code" value="" node-type="vcode" tabindex="3" /><img node-type="pincode" width="75" tabindex="4"><a node-type="changeCode" href="#" tabindex="5">换一换</a></div>
						<div class="tips WB_tips_yls WB_oauth_mobile_tips" node-type="tipBox" style="display:none">
							<a class="close" href="#0" node-type="tipClose">×</a>
							<span node-type="tipContent"></span>
						</div>
		        </div>
		       
			</form>
			
		
		<div class="btns login_btn">
		<a href="#" node-type="submit" action-type="submit"  class="btnP" tabindex="6">登录</a>
			</div>
		</div>
	</section>
	</div>
	<div class="bgbtm"></div>
	</div>
	<div class="WB_UIplus"></div> 
	<!--/登录前-->
	<script type="text/javascript" src="/oauth2/js/oauth2Mobile.js"></script>
	</body>
	</html>


第二步   


	POST https://open.weibo.cn/oauth2/authorize HTTP/1.1
	Host: open.weibo.cn
	Referer: https://open.weibo.cn/oauth2/authorize?response_type=code&scope=all&client_id=1104746493&packagename=cn.com.sina.sportslivehd&redirect_uri=http%3A%2F%2F&key_hash=22191242ac93f71da72492a63395bf40&display=mobile
	Proxy-Connection: keep-alive
	Content-Type: application/x-www-form-urlencoded
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
	Accept-Language: zh-cn
	Accept-Encoding: gzip, deflate
	Origin: https://open.weibo.cn
	Content-Length: 585
	Connection: keep-alive
	User-Agent: Mozilla/5.0 (iPad; CPU OS 7_0_4 like Mac OS X) AppleWebKit/537.51.1 (KHTML, like Gecko) Mobile/11B554a

	display=mobile&action=login&ticket=ST-MTczNzU0NDUyMQ%3D%3D-1401266758-hk-3AB1F7FAD3BD622091258D26C1751FD4&scope=all&isLoginSina=&withOfficalFlag=0&quick_auth=null&withOfficalAccount=&response_type=code&regCallback=https%253A%252F%252Fopen.weibo.cn%252F2%252Foauth2%252Fauthorize%253Fclient_id%253D1104746493%2526response_type%253Dcode%2526display%253Dmobile%2526redirect_uri%253Dhttp%253A%252F%252F%2526from%253D%2526with_cookie%253D&redirect_uri=http%3A%2F%2F&client_id=1104746493&appkey62=1MjUMl&state=&from=&offcialMobile=true&verifyToken=null&userId=qina006%40sina.cn&passwd=321456
	HTTP/1.1 200 OK
	Server: nginx/1.2.0
	Date: Wed, 28 May 2014 08:45:58 GMT
	Content-Type: text/html;charset=UTF-8
	Connection: keep-alive
	Pragma: No-cache
	Cache-Control: no-cache
	Expires: Thu, 01 Jan 1970 00:00:00 GMT
	Api-Server-IP: 10.75.25.86
	Set-Cookie: gsid_CTandWM=4uuGb76f1Mzeil0cHoOZg7i0U8p; Domain=.weibo.cn; Expires=Wed, 27-Jul-2033 08:45:57 GMT; Path=/
	Vary: Accept-Encoding
	Content-Length: 4095

	<!DOCTYPE html>
	<html>
	<head>
	<meta name="apple-mobile-web-app-capable" content="yes" />
	<meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"/>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
	<title>应用授权 - 新浪体育iPad客户端</title>
	<link href="/oauth2/css/oauthMobileV3/common.css" rel="stylesheet" type="text/css">
	</head>
	<body class="WB_widgets">
	<!--登录前-->
	<div class="container" id="outer">
	<header>
		<img src="/oauth2/images/oauthMobile/logo.png" alt="微博" width="117" height="35">
		</header>
	<section>
		<div class="W_main">
			<div class="app_info">
				<div class="app_icon">
					<img src="https://upload.api.weibo.com/square/61add42atw1eg4f3sehu5j2028028mwz.jpg" alt="">
				</div>
				<div class="app_intro">
					<h3>新浪体育iPad客户端</h3>
	                <div class="plus">
	                	新浪体育HD</div>
				</div>
			</div>
			<div class="oa_list">
				<div class="list_title">
	            	将允许 新浪体育iPad客户端 进行以下操作：
	            </div>
	            <div class="oa_ul">
						<div class="oa_li">
							获得你的个人信息，好友关系
						</div>
						<div class="oa_li">
							分享内容到你的微博
						</div>
						<div class="oa_li">
							获得你的评论
						</div>
				</div>
			</div>
			</div>
		
		<div class="W_btm W_login">
				<form name="authZForm" action="authorize" method="post" node-type="form">
					<input type="hidden" id="display" name="display" value="mobile"/>
				    <input type="hidden" name="action"  id="action" value="authorize"/>
				    <input type="hidden" name="scope"  id="scope" value="all"/>
				    <input type="hidden" name="ticket" id="ticket" value=""/>
					<input type="hidden" name="isLoginSina"  id="isLoginSina" value=""/>
					<input type="submit" style="position:absolute; top:-9999px"/>
				    <input type="hidden" name="withOfficalFlag"  id="withOfficalFlag" value="0"/>
				    <input type="hidden" name="withOfficalAccount"  id="withOfficalAccount" value=""/>
				    <input type="hidden" name="response_type" value="code"/>
				    <input type="hidden" name="regCallback" value="https%3A%2F%2Fopen.weibo.cn%2F2%2Foauth2%2Fauthorize%3Fclient_id%3D1104746493%26response_type%3Dcode%26display%3Dmobile%26redirect_uri%3Dhttp%3A%2F%2F%26from%3D%26with_cookie%3D"/>	
	       	        <input type="hidden" name="redirect_uri" value="http://"/>
	       	        <input type="hidden" name="client_id" value="1104746493"/>
	       	        <input type="hidden" name="appkey62" value="1MjUMl"/>
	       	        <input type="hidden" name="state" value=""/>
	       	        <input type="hidden" name="from" value=""/>
	       	        <input type="hidden" name="offcialMobile" value="true"/>
	       	        <input type="hidden" name="uid" value="1737544521"/>
	       	        <input type="hidden" name="url" id="url" value="https://open.weibo.cn/oauth2/authorize?response_type=code&scope=all&client_id=1104746493&packagename=cn.com.sina.sportslivehd&redirect_uri=http%3A%2F%2F&key_hash=22191242ac93f71da72492a63395bf40&display=mobile"/>
	       	        <input type="hidden" name="verifyToken" value="3a58a269332decd17ab7915730f51821"/>
	       	        <input type="hidden" name="visible" id="visible" value="0"/>
			</form>
			
			<div class="btns ctrl_btn">
				<a href="#" node-type="cancel" action-type="cancel"  class="btnG" tabindex="5">取消</a>
				<a href="#" node-type="submit" action-type="submit"  class="btnP" tabindex="6">授权</a>
			</div>
		</div>
	</section>
	<div class="bgbtm"></div>

	</div>
	<div class="WB_UIplus"></div> 
	<!--/登录前-->
	<script type="text/javascript" src="/oauth2/js/oauth2Mobile.js"></script>
	<script type="text/javascript">
		(function() {
		if(self !== top) {
		var img = new Image();
		var src = 'https://api.weibo.com/oauth2/images/bg_layerr.png?refer=' + document.referrer + '&rnd=' + (+new Date());
		img.src = src
		img = null; //释放局部变量
		}
		})();
	</script>
	</body>
	</html>


第三步   


	POST https://open.weibo.cn/oauth2/authorize HTTP/1.1
	Host: open.weibo.cn
	Accept-Language: zh-cn
	User-Agent: Mozilla/5.0 (iPad; CPU OS 7_0_4 like Mac OS X) AppleWebKit/537.51.1 (KHTML, like Gecko) Mobile/11B554a
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
	Referer: https://open.weibo.cn/oauth2/authorize
	Content-Type: application/x-www-form-urlencoded
	Connection: keep-alive
	Proxy-Connection: keep-alive
	Cookie: gsid_CTandWM=4uuGb76f1Mzeil0cHoOZg7i0U8p
	Content-Length: 775
	Origin: https://open.weibo.cn
	Accept-Encoding: gzip, deflate

	display=mobile&action=authorize&scope=all&ticket=&isLoginSina=&withOfficalFlag=0&withOfficalAccount=&response_type=code&regCallback=https%253A%252F%252Fopen.weibo.cn%252F2%252Foauth2%252Fauthorize%253Fclient_id%253D1104746493%2526response_type%253Dcode%2526display%253Dmobile%2526redirect_uri%253Dhttp%253A%252F%252F%2526from%253D%2526with_cookie%253D&redirect_uri=http%3A%2F%2F&client_id=1104746493&appkey62=1MjUMl&state=&from=&offcialMobile=true&uid=1737544521&url=https%3A%2F%2Fopen.weibo.cn%2Foauth2%2Fauthorize%3Fresponse_type%3Dcode%26scope%3Dall%26client_id%3D1104746493%26packagename%3Dcn.com.sina.sportslivehd%26redirect_uri%3Dhttp%253A%252F%252F%26key_hash%3D22191242ac93f71da72492a63395bf40%26display%3Dmobile&verifyToken=3a58a269332decd17ab7915730f51821&visible=0
	HTTP/1.1 302 Moved Temporarily
	Server: nginx/1.2.0
	Date: Wed, 28 May 2014 08:46:09 GMT
	Content-Length: 0
	Connection: keep-alive
	Pragma: No-cache
	Cache-Control: no-cache
	Expires: Thu, 01 Jan 1970 00:00:00 GMT
	Api-Server-IP: 10.75.25.86
	Location: http://?access_token=2.00dhYatBpB6lMB593d9be148B374bC&remind_in=2628831&expires_in=2628831&uid=1737544521




至此授权完成。  