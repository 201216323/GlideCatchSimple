# GlideCatchSimple

####Glide缓存Simple

1. 缓存路径的指定
2. 缓存大小的获取
3. 磁盘缓存清除(两种方法)
4. 内存缓存清除

* 可clone之后查看使用Simple

####Glide cache Simple.

1. The cache path specified
2. The cache size
3. The disk cache (two ways)
4. Memory cache to clearMay

* use Simple clone after check

####GlideCatchUtil
获取Glide磁盘缓存大小
```
public String getCacheSize() {
    try {
        return getFormatSize(getFolderSize(new File(Application.getInstance().getCacheDir() + "/" + GlideCatchConfig.GLIDE_CARCH_DIR)));
    } catch (Exception e) {
        e.printStackTrace();
        return "获取失败";
    }
}
```
清除Glide磁盘缓存
```
public boolean cleanCatchDisk() {
    return deleteFolderFile(Application.getInstance().getCacheDir() + "/" + GlideCatchConfig.GLIDE_CARCH_DIR, true);
}

public boolean clearCacheDiskSelf() {
    try {
        if (Looper.myLooper() == Looper.getMainLooper()) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    Glide.get(Application.getInstance()).clearDiskCache();
                }
            }).start();
        } else {
            Glide.get(Application.getInstance()).clearDiskCache();
        }
        return true;
    } catch (Exception e) {
        e.printStackTrace();
        return false;
    }
}
```
AndroidMainfest.xml and GlideConfiguration.class
```
<meta-data
    android:name="com.yaphetzhao.glidecatchsimple.glide.GlideConfiguration"
    android:value="GlideModule" />
```
Application.class
```
public class Application extends android.app.Application {

    public static Application instance;

    public static Application getInstance() {
        return instance;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        instance = this;
    }

}

<application
    android:name=".Application"
    more...
```

####About Me
YaphetZhao
Email:yaphetzhao@gmail.com
Email_CN:yaphetzhao@foxmail.com
GitHub:http://github.com/YaphetZhao/
QQ:11613371
CSDN_Blog:http://blog.csdn.net/yaphetzhao