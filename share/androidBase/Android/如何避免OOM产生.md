如何避免OOM产生

##### OOM如何产生？

- 已使用内存+新申请内存>可分配内存
- 通常指堆内存
- Native Heap物理内存不够时也会产生

##### 如何减少产生？

- 使用适合的数据结构：

  HashMap：增删频繁会好很多

  SoarseArray: Key是整形

  ArrayMap: 因泛型的开箱与关箱操作

- 避免使用枚举

  Enum: 24Bytes 

  Int: 4Bytes

  枚举不多的时候，用Int替代吧

- Bitmap 的使用

  选择合适的分辨率

  原始文件与内存缩放的结果，与屏幕密度有关；

  不使用帧动画，尽量使用代码实现动效

  Bitmap的重采样和复用配置（减少内存开辟以免GC）；

- 小心使用多进程

  每个进程被fork出来的时候先天带有公共系统预加载资源，如果进程的功能少或者是代码少，那么建议合并；

- 谨慎使用LargeHeap

  Android:largeHeap="true" ,每个手机Rom不一样；堆大会影响GC的回收效率；

- 使用NDK需要合理控制内存使用

  NativeHeap本身是无内存使用限制，但别花冒了；

  对于一些内存需求较强的可做到Native层；

  

  ##### 内存优化的5R法则（Tencent-胡凯）

  Reduce缩减：降图片分辨率/重采样

  Reuse: 复用减少GC

  Recycle回收： 主动销毁控制，避免内存泄漏，控制好生命周adet

  Refactor: 合适的数据结构、更合适的程序架构

  Revalue重审：谨慎使用LargeHeap/多进程/第三方框架



Android性能优化典范：

android performance patterns

https://www.youtube.com/watch?v=qk5F6Bxqhr4&list=PLWz5rJ2EKKc9CBxr3BVjPTPoDPLdPIFCE



