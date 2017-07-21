---
title: 唱吧获取mp3下载地址
date: 2017-05-23 10:36:28
tags: [脚本]
categories: [脚本]
---

# 具体使用方法
* 代码中userid可以通过F12，查看网页源码找到，该脚本需要打开唱吧的页面才能调用，可以通过Chrome的console调用。

# 代码--此代码网上搜的，不过找不到原作者网址了

<!--more-->

```javascript

var list = [],
loadSongsUrl = "http://changba.com/member/personcenter/loadmore.php?pageNum=#pageNo#&type=0&userid=?",
loadPlayUrl = "http://changba.com/member/personcenter/loadplayurl.php?wid=#wid#",
matchMp3Reg = /http:\/\/.*?\.changba\.com\/.*?\d+\.mp3/g;
var loadSongsCallback = function(pageNo,data,respText,defered){
	if(respText=='success'&&data.length){
		loadMoreSongs(++pageNo);
	}else{
		//console.log(list);
		loadPlayUrlInfo(0);
	}
}
var loadMoreSongs = function  (pageNo) {
	$.getJSON(loadSongsUrl.replace('#pageNo#',pageNo),null,function(data) {
		list = list.concat(data);
	}).done(function(data,respText,defered){
		loadSongsCallback.call(this,pageNo,data,respText,defered);
	});
}

var loadPlayUrlCallback = function(idx,data,respText,defered){
	console.log('loading ' + idx +'/'+list.length+' song play url');
	if(respText=='success'&&idx<list.length-1){
		loadPlayUrlInfo.call(this,++idx);
	}else{
		//console.log(list);
		loadMp3UrlInfo(0);
	}
}
var loadPlayUrlInfo = function(idx) {
	var song = list[idx];
	$.get(loadPlayUrl.replace('#wid#',song.workid),null,function(data) {
		song.playUrl = data;
	}).done(function(data,respText,defered){
		loadPlayUrlCallback.call(this,idx,data,respText,defered);
	});
}

var loadMp3UrlCallback = function(idx,data,respText,defered){
	console.log('loading ' + idx +'/'+list.length+' song mp3 url');
	if(respText=='success'&&idx<list.length-1){
		loadMp3UrlInfo.call(this,++idx);
	}else{
		console.log(list);
		//console.log(JSON.stringify(list))
	}
}
var loadMp3UrlInfo = function(idx) {
	var song = list[idx];
	$.get(song.playUrl,null,function(data) {
		var match = data.match(matchMp3Reg);
		song.mp3Url = (match && match[0]);
	}).done(function(data,respText,defered){
		loadMp3UrlCallback.call(this,idx,data,respText,defered);
	});
}

loadMoreSongs(0);
```
