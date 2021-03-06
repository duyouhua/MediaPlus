# MediaPlus  

<div align=left>
<img width="100" height="100" src="https://github.com/javandoc/MediaPlus/blob/master/Resource/MediaPlus_2.png"/>
</div>

#### android 音视频采集与推流：
* [releases](https://github.com/javandoc/MediaPlus/releases/)

* [文档链接](https://juejin.im/user/5809cf500bd1d00057ddc475)

<div align=center>
<img src="https://github.com/javandoc/MediaPlus/blob/master/Resource/MediaPlus_xmind.png"/>
</div>


* Rtmp推流截图
<div align=center>
<table border=0 cellspacing="10" style="border-collapse:separate; border-spacing:0px 50px;">
<td>
<img width="220" height="380" src="https://github.com/javandoc/MediaPlus/blob/master/Resource/screen_one.png"/>
</td>
<td>
<img width="220" height="380" src="https://github.com/javandoc/MediaPlus/blob/master/Resource/screen_live.gif"/>
</td>
</table>

</div>

* 水印截图
<div align=center>
<table border=0 cellspacing="10" style="border-collapse:separate; border-spacing:0px 50px;">
<td>
<img width="220" height="380" src="https://github.com/javandoc/MediaPlus/blob/master/Resource/watermark.gif"/>
</td>
</table>
</div>



* Android相机采集NV21格式数据，并使用libyuv转换I420（yuv420p）、处理I420旋转、前置摄像头镜像; 音频采集PCM数据：2通道、16位、采样率48000KHz,音视频软编。
* 当前版本支持RTMP协议推流。
* 支持视频添加水印功能。
* 适用于Android移动音频和视频的采集和推流。
* 暂无任何视频滤镜等其他特效。
* 搭建RTMP测试服务(如:nginx+rtmp、crtmpserver、Red5等);也可以写入本地文件，只需更改推流地址，如：“/mnt/sdcard/test.flv”。


#### JNI 核心 API说明：
```

* 初始化音视频采集
LiveJniMediaManager.InitAudioCapture(int channles, int SampleRate, int SampleBitRate);
LiveJniMediaManager.InitVideoCapture(int inWidth, int inHeight, int outWidth, int outHeight, int fps, boolean mirror);
	
* 初始化音视频编码器
LiveJniMediaManager.InitAudioEncoder();
LiveJniMediaManager.InitVideoEncoder();

* 水印添加
LiveJniMediaManager.SetWaterMark(boolean enable,byte[] waterMark,int waterWidth,int waterHeight,int positionX,int positionY);
    
* 开始推流
LiveJniMediaManager.StartPush(pushUrl);
        
* 发送音视频数据至底层
LiveJniMediaManager.EncodeH264(videoBuffer, length);
LiveJniMediaManager.EncodeAAC(audioBuffer, length);
 
* 停止推流与资源回收
LiveJniMediaManager.Close();
LiveJniMediaManager.Release();

   
```

#### RtmpPushStreamer使用示例:
```
 mRtmpPushStreamer = new RtmpPushStreamer.Builder()
                     .withActivity(LiveActivity.this)
                     .withSurfaceView(surfaceView)
                     .withWaterMark(true, ivWaterMark, 90, 30)  //参数:true 水印开关 水印图片 宽(90px)\高(30px)
                     .withPushStreamCall(new PushStreamCall() {
                            @Override
                            public void PushSucess() {                     
                               #-------"推流成功"--------#
                            }

                            @Override
                            public void PushFailed() {
                               #-------"推流失败"--------#
                            }
                        }).build();
```

#### -- [download APK](https://github-production-release-asset-2e65be.s3.amazonaws.com/107510291/bcd624bc-d9dc-11e7-9e0c-e07b0b4de0d4?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20171205%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20171205T085701Z&X-Amz-Expires=300&X-Amz-Signature=4cf701cb8efb7e4f46d093a34b2962d6e572dba48e7a208d74879fb059f41d58&X-Amz-SignedHeaders=host&actor_id=9412054&response-content-disposition=attachment%3B%20filename%3Dapp-debug.apk&response-content-type=application%2Fvnd.android.package-archive) --

#### -- [API文档](https://javandoc.github.io/javadoc/) --
