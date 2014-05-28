---
title:  微博sdk授权app过程
author: hacker
layout: post
permalink:  /weibo-sdk-authorize-app/
tags:
  - 移动
  - 授权
---




微博sdk授权app三步走（微盘为例）


一般应用通过微博sdk来获取最终的access token需要遵循三步走的步骤，最终通过oauth2拿到授权。
<!--more-->

第一步


	POST http://api.weibo.cn/2/account/login?c=android&wm=3333_1001&imei=352315050333919&did=85882ab1851092f1d0f17d2a2bafb15d6b343efd&device_id=85882ab1851092f1d0f17d2a2bafb15d6b343efd&from=1043595010&skin=default&i=90ec00d&device_name=samsung-GT-I9300&s=72575b7c&gsid=4uQJ043f3siw3338MakJTcy7Uca&trim_user=1&ua=samsung-GT-I9300__weibo__4.3.5__android__android4.0.4&oldwm=3333_1001&lang=zh_CN HTTP/1.1
	User-Agent: GT-I9300_4.0.4_weibo_4.3.5_android
	Accept-Encoding: gzip,deflate
	X-Log-Uid: 2991122754
	Content-Length: 823
	Content-Type: multipart/form-data; boundary=F5MxOxZhm4IgnI1Dg3uVXFO49ufz9WEVD8OqmDl
	Host: api.weibo.cn
	Connection: Keep-Alive

	--F5MxOxZhm4IgnI1Dg3uVXFO49ufz9WEVD8OqmDl
	Content-Disposition: form-data; name="did"
	Content-Type: text/plain; charset=UTF-8
	Content-Transfer-Encoding: 8bit

	85882ab1851092f1d0f17d2a2bafb15d
	--F5MxOxZhm4IgnI1Dg3uVXFO49ufz9WEVD8OqmDl
	Content-Disposition: form-data; name="device_id"
	Content-Type: text/plain; charset=UTF-8
	Content-Transfer-Encoding: 8bit

	85882ab1851092f1d0f17d2a2bafb15d6b343efd
	--F5MxOxZhm4IgnI1Dg3uVXFO49ufz9WEVD8OqmDl
	Content-Disposition: form-data; name="device_name"
	Content-Type: text/plain; charset=UTF-8
	Content-Transfer-Encoding: 8bit

	samsung-GT-I9300
	--F5MxOxZhm4IgnI1Dg3uVXFO49ufz9WEVD8OqmDl
	Content-Disposition: form-data; name="imei"
	Content-Type: text/plain; charset=UTF-8
	Content-Transfer-Encoding: 8bit

	352315050333919
	--F5MxOxZhm4IgnI1Dg3uVXFO49ufz9WEVD8OqmDl--


	HTTP/1.1 200 OK
	Date: Wed, 28 May 2014 02:37:46 GMT
	Server: Apache
	X-Log-Uid: 2991122754
	Vary: Accept-Encoding
	x-debug: 172.16.139.134
	Content-Length: 405
	Connection: close
	Content-Type: application/json;charset=UTF-8
	SINA-LB: aGwuMTQyLnNnMS5oeWRzLmxiLnNpbmFub2RlLmNvbQ==
	SINA-TS: Nzc2OWMzNjggMCA1MiA1MiA4IDE2Nwo=

	{"screen_name":"_\u74b0v\u5427\u56de\u6b78v\u500b","oauth_token":"d6523791ebce57e4ace9d33e34dba90f","oauth_token_secret":"4031ed3c321f922cd1fb973011fae7aa","oauth2.0":{"access_token":"2.005f87QDMhHgLIea4ac7f3a2vrIrNC","issued_at":1400209563,"expires":1614135},"gsid":"4uQJ043f3siw3338MakJTcy7Uca","status":1,"uid":"2991122754","url":"http:\/\/weibo.cn","msg_url":"http:\/\/weibo.cn\/msg","interceptad":""}

第二步


	GET http://api.weibo.cn/2/users/show?uid=2991122754&s=72575b7c&gsid=4uQJ043f3siw3338MakJTcy7Uca&c=android&wm=3333_1001&has_member=1&ua=samsung-GT-I9300__weibo__4.3.5__android__android4.0.4&oldwm=3333_1001&from=1043595010&sourcetype=feed&skin=default&has_extend=1&i=90ec00d&lang=zh_CN HTTP/1.1
	User-Agent: GT-I9300_4.0.4_weibo_4.3.5_android
	Accept-Encoding: gzip,deflate
	X-Log-Uid: 2991122754
	Host: api.weibo.cn
	Connection: Keep-Alive


	HTTP/1.1 200 OK
	Date: Wed, 28 May 2014 02:37:47 GMT
	Server: Apache
	X-Log-Uid: 2991122754
	Vary: Accept-Encoding
	x-debug: 10.13.0.129
	Content-Length: 2537
	Connection: close
	Content-Type: application/json;charset=UTF-8
	SINA-LB: aGwuMTQyLnNnMS5oeWRzLmxiLnNpbmFub2RlLmNvbQ==
	SINA-TS: NzBlMmRlY2UgMCA1MyA1MyA3IDEwOAo=

	{"id":2991122754,"idstr":"2991122754","class":1,"screen_name":"_\u74b0v\u5427\u56de\u6b78v\u500b","name":"_\u74b0v\u5427\u56de\u6b78v\u500b","province":"11","city":"8","location":"\u5317\u4eac","description":"","url":"","profile_image_url":"http:\/\/tp3.sinaimg.cn\/2991122754\/50\/5670662362\/0","profile_url":"u\/2991122754","domain":"","weihao":"","gender":"\u5973","followers_count":20,"friends_count":12,"statuses_count":160,"favourites_count":0,"created_at":"Mon Sep 17 15:48:05 +0800 2012","following":false,"allow_all_act_msg":false,"geo_enabled":true,"verified":false,"verified_type":-1,"remark":"","status":{"created_at":"Mon May 19 15:54:34 +0800 2014","id":3711969992973663,"mid":"3711969992973663","idstr":"3711969992973663","text":"\u5206\u4eab\u56fe\u7247 \u6211\u5728\u8fd9\u91cc:http:\/\/t.cn\/8kQd2Cm","source":"<a href=\"http:\/\/app.weibo.com\/t\/feed\/4d8JpP\" rel=\"nofollow\">\u4e09\u661fGalaxy SIII<\/a>","favorited":false,"truncated":false,"in_reply_to_status_id":"","in_reply_to_user_id":"","in_reply_to_screen_name":"","pic_ids":["b248e942jw1egjmz2huh5j20k00zkgqf"],"thumbnail_pic":"http:\/\/ww3.sinaimg.cn\/thumbnail\/b248e942jw1egjmz2huh5j20k00zkgqf.jpg","bmiddle_pic":"http:\/\/ww3.sinaimg.cn\/bmiddle\/b248e942jw1egjmz2huh5j20k00zkgqf.jpg","original_pic":"http:\/\/ww3.sinaimg.cn\/large\/b248e942jw1egjmz2huh5j20k00zkgqf.jpg","geo":null,"annotations":[{"place":{"poiid":"SQ100043","lon":116.316422,"title":"\u4e2d\u5173\u6751","type":"checkin","lat":39.983879},"client_mblogid":"413051f0-a2e5-4521-b4ca-e4d8aeb0a92e"}],"reposts_count":0,"comments_count":0,"attitudes_count":0,"mlevel":0,"visible":{"type":0,"list_id":0}},"ptype":0,"allow_all_comment":true,"avatar_large":"http:\/\/tp3.sinaimg.cn\/2991122754\/180\/5670662362\/0","avatar_hd":"http:\/\/ww3.sinaimg.cn\/crop.36.36.108.108.1024\/b248e942jw1e7bwx52omlj2050050q34.jpg","verified_reason":"","verified_trade":"","verified_reason_url":"","verified_source":"","verified_source_url":"","follow_me":false,"online_status":0,"bi_followers_count":3,"lang":"zh-cn","star":0,"mbtype":0,"mbrank":0,"block_word":0,"block_app":0,"level":1,"type":1,"ulevel":0,"badge":{"kuainv":{"level":0},"uc_domain":0,"enterprise":0,"anniversary":0,"taobao":0,"travel2013":0,"gongyi":0,"gongyi_level":0,"bind_taobao":0,"hongbao_2014":0,"suishoupai_2014":0,"worldcup_2014":0,"worldcup_country":0},"extend":{"privacy":{"mobile":1},"mbprivilege":"0000000000000000000000000000000000000000000000000000000000000000"},"worldcup_guess":0,"member_type":0,"cover_image_phone_level":1}


第三步


	GET https://open.weibo.cn/oauth2/authorize?client_id=1396484607&redirect_uri=http://2.vauth.appsina.com/callback.php&display=mobile&response_type=code&access_token=2.005f87QDMhHgLIea4ac7f3a2vrIrNC&packagename=com.sina.VDisk&key_hash=afb5b050a772afa3462150929183491d&scope=email,direct_messages_read,direct_messages_write,friendships_groups_read,friendships_groups_write,statuses_to_me_read,follow_app_official_microblog HTTP/1.1
	Host: open.weibo.cn
	Connection: keep-alive
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
	User-Agent: Mozilla/5.0 (Linux; U; Android 4.0.4; zh-cn; GT-I9300 Build/IMM76D) AppleWebKit/534.30 (KHTML, like Gecko) Version/4.0 Mobile Safari/534.30
	Accept-Encoding: gzip,deflate
	Accept-Language: zh-CN, en-US
	Accept-Charset: utf-8, iso-8859-1, utf-16, gb2312, gbk, *;q=0.7


	HTTP/1.1 302 Moved Temporarily
	Server: nginx/1.2.0
	Date: Wed, 28 May 2014 02:37:50 GMT
	Content-Length: 0
	Connection: keep-alive
	Pragma: No-cache
	Cache-Control: no-cache
	Expires: Thu, 01 Jan 1970 00:00:00 GMT
	Api-Server-IP: 10.75.2.82
	Location: http://2.vauth.appsina.com/callback.php?access_token=2.005f87QDR8VVWB86139e085e0DGTXF&remind_in=2650929&expires_in=2650929&refresh_token=2.005f87QDR8VVWB6fcb33ede6lIj9_D&uid=2991122754



至此授权完成。