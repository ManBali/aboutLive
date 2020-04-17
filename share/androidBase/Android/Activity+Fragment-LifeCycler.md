Activity+Fragment 生命周期

##### Activity大致生命周期

```java
onCreate

onStart

onResume

onPause

onStop

onDestory
```

###### onStart与onResume区别

onStart是可见，但还不能交互（不可用）

onResume:可见可交互

###### 一个标准的Activity按Home按键与Back按键的生动周期变化

Home: onPause->onStop   如果再回来应用其生命周期：onRestart-->onStart-->onResume 

Back: onPause->onStop->onDestory

###### Stand模式的Activity A,B 两页面，由A打开B，其整个的生命周期

A.onPause-->B.onCreate->B.onStart->B.onResume->

A.Stop



##### Fragment启动生命周期

较Activity的区别在于onCreate与onDestory的一些区别

onCreate:变成了  onAttach->onCreate-->onCreateView-->onViewCreated

onDestory变成了：onDestoryView-->onDestory->onDetach

所以整体的生命周期大致如下

```java
onAttach
  onCreate
  onCreateView
  onViewCreated
onStart
  onResume
onPause
  onStop
onDestoryView
  onDestory
  onDetach
```

> https://jingyan.baidu.com/article/48b558e3035d9a7f38c09aeb.html







