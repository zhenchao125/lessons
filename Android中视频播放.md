# Android中视频播放

> 在Android中有三种方式实现视频的播放
1. 使用Android系统自带播放器。指定Action为ACTION_VIEW,Data为Uri，Type为其MIME类型。
2. 使用VideoView来播放。在布局文件中使用VideoView结合MidiaController来控制。
3. 使用MedioPlayer和SurfaceView来实现。这种方式最灵活。

----------------------------------------------------------

### 一、使用Android系统自带播放器播放视频

```
Uri uri = Uri.fromFile(new File(Environment.getExternalStorageDirectory(), "a.mp4"));
Intent intent = new Intent();
intent.setAction(Intent.ACTION_VIEW);
intent.setDataAndType(uri, "video/*");
startActivity(intent);
```
-------------------------------------------------------------

### 二、使用VideoView播放
> 布局文件。在相应的布局文件中添加VideoView

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <VideoView
        android:id="@+id/videoView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</LinearLayout>
```

> 播放本地视频代码

```
videoView = (VideoView) findViewById(R.id.videoView);
Uri uri = Uri.fromFile(new File(Environment.getExternalStorageDirectory(), "a.mp4"));
videoView.setMediaController(new MediaController(this)); //关联MediaController
videoView.setVideoURI(uri); //设置视频文件的Uri
videoView.requestFocus();  //让videoView获取到焦点
videoView.start(); //开始播放视频
```
> MediaController的一些方法

*MediaController 继承自FrameLayout，显示视频的控制组件的。如下图*

![图片](https://github.com/zhenchao125/imgs/blob/master/player.jpg?raw=true)

```
MediaController controller = new MediaController(this);
controller.hide();  //隐藏控制组件
controller.show(1000);  //显示控制组件。 1s之后自动隐藏。如果此处传入0，则代表不会自动隐藏。
controller.show();  //显示控制组件。  默认3s之后会自动隐藏

```


#
#
#
