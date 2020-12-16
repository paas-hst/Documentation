# 高级功能


## 视频渲染拉伸模式的选择

设置视频模式合成布局时，会遇到里面的视频有黑边或显示不全的情况，此时要根据视频的分辨率进行考虑。通过crop_mode控制视频的显示模式。
比如一个16:9的视频，放到4:3的窗口里。如果选择等比裁剪，则左右会有部分看不见。如果选择等比居中，则上下有黑边。如果选择缩放平铺，则上下会被拉伸，视频会有一点变形。

<img alt="appid.png" src="http://fs.hst.com/download/paas/images/documentation/crop_example.jpg" align="center" />

