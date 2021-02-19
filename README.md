# -x5-webview

介绍:
====
      集成了腾讯x5,添加了启动图和倒计时,启动图过后就是一个全屏webview了,类似于HBuilder X里面的

      wab2app,通过一个网址就能打包属于自己的webapp,集成腾讯x5内核解决了很多原生webview出现的问题

      成品实例:
      
      参考项目里的 app_debug.apk
      
功能:
====
      1.集成腾讯x5内核
            
      2.使用TBS接管视频播放

      3.接入文件浏览能力,可以选择文件上传

      4.打开某些网址不会跳转到浏览器

      5.解决启动图过后加载网页会白屏一段时间的问题
      
      6.解决启动应用的一瞬间短暂白屏问题


导入:
====
      相信大家都有一个共同的烦恼,就是从别人仓库里拉取过来的项目会报各种错误,为此我也研究出解决方案:
      
      1.第一步项目完整的拉取下来使用android studio打开,如果报错就先根据错误做处理再进行第二步
      
      2.如果确实没有能力处理报错,可以尝试新建一个新项目,一般来说空项目都是可以直接运行的,然后导入拉取下来项目的module 或许可以解决一些问题
      
      3.如果上述操作没有解决你的问题,您可以直接创建一个新项目,删除moudule的main目录,替换成拉取下来的项目的main目录


项目结构介绍:
============
      只有两个类,也就是两个activity
     
      StartImage类:启动图页面,初始化x5内核,和控制倒计时秒数,默认是3秒,如果需要修改秒数请修改成员变量 count的值即可
      
      Home类:装载腾讯x5组件,初始化一些配置,如去掉视频播放的分享按钮,接入文档浏览能力等,如果需要更换网址,只需要修改成员变量的url的值即可
      
      启动图片修改:android的资源文件分别有两图片
      
      icon.jpg:应用图标
      start.jpg:启动图片
      
      应用名称修改:AndroidManifest.xml里面的android:label="应用名称"修改即可



项目遇到到的一些问题:
======================
      1.如今的x5内核引用很简单,通过implementation 'com.tencent.tbs.tbssdk:sdk:43903'引入即可
      
      2.腾讯x5内核第一次加载必须在一个单独的activity里进行初始化,我曾尝试只用一个类来使用,启动页使用fragment来实现,但是不如意的是
      
      腾讯x5内核第一次加载是失败的,原因是加载腾讯x5内核是一个异步线程,但是通常还没加载成功,x5的组件就被加载了自动切换成了内置webview,
      所以这里使用单独的activity也就是StartImage来初始化内核,内核加载完毕后再去跳转到Home的activity,就不会出现这样的问题.
