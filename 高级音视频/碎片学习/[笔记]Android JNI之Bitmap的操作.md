### [笔记]Android JNI之Bitmap的操作

原博客：https://mp.weixin.qq.com/s/2ilXU9UocjcrHR-q8Ao45w

####  1、解决的问题？

* 了解jni集成bitmap库，集成头文件bitmap.h
* 了解bitmap.h基本的函数  

```
AndroidBitmap_getInfo ,检索 Bitmap 对象信息,，第一个参数就是 JNI 接口指针，第二个参数就是 Bitmap 对象的引用，第三个参数是指向 AndroidBitmapInfo 结构体的指针。
AndroidBitmap_lockPixels,访问原生像素缓存
AndroidBitmap_unlockPixels  释放原生像素缓存
```

* bitmap的旋转（反射调用java类，生成Bitmap与Bitmap.Config）

  读取原有bitmap的像素内容进行奥做后再复制给新的Bitmap

  上下翻转，左右镜像

#### 2 、涉及的知识点？

- JNI，JNI反射调用java类(java成员类)
- Bitmap的基本函数操作，以及数据如何实现左右旋转和镜像

#### 3、 提取重点内容，比如问题发生的缘由，有哪几种解决办法？

##### 方案1：Matrix直接操作，Bitmap.createBitmap

##### 方案2：画布Canvas+Matrix进行左右旋转（Canvas.drawBitmap）

网上有别人的测试结果

方法1在280 - 350毫秒间， 方法2在110毫秒左右。
