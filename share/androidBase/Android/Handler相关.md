Handler+Message+MessageQueen+Looper

要了解Handler，就首先需要了解Android的消息传递机制，整个消息传递机制有四部分组成：

##### 1.Message 

消息，即线程间传递的对象，传递的信息包含在其中。例如后台线程在处理数据完毕后需要更新UI，则可发送一条包含更新信息的Message给UI线程。 

##### 2. Message Queue 

消息队列，用来存放通过Handler发布的消息，按照先进先出执行。 

##### 3. Handler 

Handler是Message的主要处理者，负责将Message添加到消息队列以及对消息队列中的Message进行处理。 

##### 4. Looper 

循环器，扮演Message Queue和Handler之间桥梁的角色，循环取出Message Queue里面的Message，并交付给相应的Handler进行处理。





### 如何实现线程之间切换

###### 最终回到Handler是如何实现线程之间的切换的呢？例如现在有A、B两个线程，在A线程中有创建了handler，然后在B线程中调用handler发送一个message。

通过上面的分析我们可以知道，当在A线程中创建handler的时候，同时创建了MessageQueue与Looper，Looper在A线程中调用loop进入一个无限的for循环从MessageQueue中取消息，当B线程调用handler发送一个message的时候，会通过msg.target.dispatchMessage(msg);将message插入到handler对应的MessageQueue中，Looper发现有message插入到MessageQueue中，便取出message执行相应的逻辑，因为Looper.loop()是在A线程中启动的，所以则回到了A线程，达到了从B线程切换到A线程的目的。



### 总结

------

1.Handler初始化之前，Looper必须初始化完成。UI线程之所以不用初始化，因为在ActivityThread已经初始化，其他子线程初始化Handler时，必须先调用Looper.prepare()。

2.通过Handler发送消息时，消息会回到Handler初始化的线程，而不一定是主线程。

3.使用ThreadLocal时，需要注意内存泄漏的问题。



### 通俗点的说法Handler机制其实就是借助共享变量来进行线程切换的.

