 **Service的生命周期，两种启动方法，有什么区别**

##### startService

onCreate-->onStartCommand-->running-->onDestory-->onStop

startService/stopService

其中：onCreate只执行一次，onStartCommand可执行多次

##### bindService

