# 高级功能


## 视频渲染拉伸模式的选择

设置视频模式合成布局时，会遇到里面的视频有黑边或显示不全的情况，此时要根据视频的分辨率进行考虑。通过crop_mode控制视频的显示模式。
比如一个16:9的视频，放到4:3的窗口里。如果选择等比裁剪，则左右会有部分看不见。如果选择等比居中，则上下有黑边。如果选择缩放平铺，则上下会被拉伸，视频会有一点变形。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/documentation/crop_example.jpg" align="center" />


## 主动控制视频布局

当自动录制无法满足客户的录制场景时，客户可以通过调用布局接口[设置合成效果]来主动控制视频和音频的混合结果。

以4位用户音视频沟通的内容录制下来为案例，需要理解以下内容：
接口通过一个平面坐标轴确定视频的可视位置。左上角为原点(0,0),从左往右x逐渐增加，从上往下y逐渐增加。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/documentation/axis.jpg" align="center" />

接口参数里的核心控制参数为audio_list和video_list，audio_list对合成的音频内容进行控制。video_list对合成的视频以及其位置、大小进行控制。
把4位用户的音频、视频信息作为参数列入设置合成接口里。

```js
{
"business":"RE",
"id":"4102",
"record_id":"XXXXXXXX",
"audio_list":{
	{"user_id":"Jack_ID","media_id":1},
	{"user_id":"Paul_ID","media_id":1},
	{"user_id":"Ana_ID","media_id":1},
	{"user_id":"James_ID","media_id":1}
	},
"video_list":{
	{"user_id":"Jack_ID","media_id":0,"media_type":2,"crop_mode":3,"w":530,"h":380},
	{"user_id":"Paul_ID","media_id":0,"media_type":2,"crop_mode":3,"x":531,"w":530,"h":380},
	{"user_id":"Ana_ID","media_id":0,"media_type":2,"crop_mode":3,"y":381,"w":530,"h":380},
	{"user_id":"James_ID","media_id":0,"media_type":2,"crop_mode":3,"x":531,"y":381,"w":530,"h":380}
	},
"seq":""
}
```

需要知道每个视频的视频区域大小，分配的视频区域过大或过小都不合适。过大时，视频会因为拉伸而模糊；过小时，视频会被压缩而看不清细节。
服务器会按照设置的crop_mode值在指定位置填充视频。
命令发送成功后，录制效果会被设置成“田”字来录制四路视频以及他们的音频内容。完成录制后的效果如下。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/documentation/layout_4.jpg" align="center" />





## 视频增加说明或用户名字

录制下的视频可能需要加上视频对应的用户名，方便查看的时候知道每个视频属于谁的。可以通过[设置视频水印与字幕](http://)接口实现。
在控制布局后，可以单独调用水印功能。实现在视频上叠加用户名的效果。
注意：content里填写的是内容，而不是像前面audio_list,video_list里的user_id用户ID。

```js
{
"business":"RE",
"id":"4103",
"record_id":"XXXXXXXX",
"subtitle_list":{
	{"content":"Jack","color":#009cff,"x":20,"y":50},
	{"content":"Paul","color":#009cff,"x":540,"y":50},
	{"content":"Ana","color":#009cff,"x":20,"y":440},
	{"content":"James","color":#009cff,"x":540,"y":440}
	},
"seq":""
}
```

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/documentation/record_name.jpg" align="center" />

## 录制结束/上传完成回调

录制任务除了手动触发结束，也会节省资源自动结束。注意监听录制结束回调，已方便做后续的处理，比如上传完成后，下载视频到本地。



## 视频可查看时机

视频录制完是需要一定时间处理的。并不是录制完就可以立刻查看。建议第二天进行查看。
也可以等待文件完成时的回调，让服务器根据回调再去做后续的事情。