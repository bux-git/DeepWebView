# DeepWebView
WebView记录
### 一.Webview常见的坑
    1.Android API level 16 以及之前的版本存在远程代码执行安全漏洞，
      该漏洞源于程序没有正确限制使用WebView.addJavascriptInterface方法，
      远程果农国际者可以通过使用Java Reflection API利用漏洞执行任意Java对象的方法

    2.WebView在布局文件中使用时：WebView写在其他容器中时当离开界面时销毁webView否则将造成内存泄漏问题,
      先 从容器布局中removewebView，然后调用WebView.removeAllViews(),在调用WebView的destroy方法     

    3.jsbridge  实现java和js的互相调用的桥梁
    
    4.
    
    WebViewClient.onPageFinished
     加载页面完成时会回调此方法
     这个方法会判断当前网页内容是否加载完毕，当前网页正在加载时，又进行了跳转 此方法会回调很多次
     因此需要尽量避免在onPageFinished()中做业务操作，否则会导致重复调用，还有可能会引起逻辑上的错误.
 
    WebChromeClient.onProgressChanged
     表示当前页面的加载速度，比onPageFinished靠谱一些
 
    5.后台耗电
     程序开启WebView时，WebView会自动开启一些线程 导致耗电严重
     粗暴方法，在Activity onDestory中 调用system.exit();直接把虚拟机关闭
 
    6.WebView硬件加速导致页面渲染问题
      会导致页面出现白块 闪烁问题，解决方法只能暂时关闭硬件加速
 
 
### 二.关于WebView的内存泄漏问题
    
    WebView关联activity webview在新立线程中执行
     activity无法确定webview执行时间，导致weview一直持有activity引用
     和匿名内部类只有外部类引用一样
 
    1.独立进程，简单暴力，可能涉及到进程间通信
    2.动态添加WebView，对传入WebView中使用的Context使用若应用，动态添加WebView意思在
      布局创建哥ViewGroup用来放置WebView，Activity创建时add进来，在Activity停止时remove掉
      
[《WebView使用详解（一）——Native与JS相互调用（附JadX反编译）》 ](http://blog.csdn.net/harvic880925/article/details/51464687)    
[《WebView使用详解（二）——WebViewClient与常用事件监听》](http://blog.csdn.net/harvic880925/article/details/51523983)    
[WebView使用详解（三）——WebChromeClient与LoadData补充](http://blog.csdn.net/harvic880925/article/details/51583253)    
[]()