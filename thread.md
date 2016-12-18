# Java 线程
### 进程与线程的区别
>概念具体度娘，进程比喻为：车间，每个车间都有自己独立的存储空间；线程比喻为：车间的的流水线，线程是共享内存空间。因此需要进行线程同步，否则可能会造成数据不一致。

### 线程的定义及使用
>方式一：线程的定义，实现Runnable接口,重写run方法

```
public Class MyThread implements Runnable {//定义线程类
	
	//线程类的属性
	private 类型 属性名;

	@Override
	public void run() {//线程启动后执行run方法
		//线程具体工作内容
	}

	//线程类的方法

}

```
>方式一：线程的使用

```
public Class Test {

	public static void main(String[] args) {
		//实例化线程类
		MyThread myThread = new MyThread();//调用无参数构造方法
		//创建线程
		Thread thread_A = new Thread(myThread,"线程名称");
		//线程创建后处于New状态，需要切换到runnable状态，等待cpu调度执行
		thread_A.start();//调用Thread类start方法，线程处于可运行状态,具体什么时候运行，取决于cpu的调度情况
		//再次创建一个新的线程
		Thread thread_B = new Thread(myThread,"线程名称");
		//线程创建后处于New状态，需要切换到runnable状态，等待cpu调度执行
		thread_B.start();//调用Thread类start方法，线程处于可运行状态,具体什么时候运行，取决于cpu的调度情况
	}
}

```

>方式二：继承Thread对象

```
public Class MyThread extends Thread {//定义线程类
	
	//线程类的属性
	private 类型 属性名;

	@Override
	public void run() {
		//线程具体工作内容
	}

	//线程类的方法

}
```
>方式二：线程的使用

```
public Class Test {

	public static void main(String[] args) {
		//实例化线程类
		MyThread myThreadA = new MyThreadA();//调用无参数构造方法
		myThreadA.start();//创建一个线程，线程启动后执行run方法
		//再次创建线程
		MyThread myThreadB = new MyThreadB();//调用无参数构造方法
		myThreadB.start();//创建一个线程，线程启动后执行run方法
	}
}

```

### 两种线程创建方式的区别
* java只单继承,采用extends会受限于java单继承
* java单继承创建的线程，熟悉jvm内存分配机制的话，单继承的方式无法实现内存共享
* 采用implements解决单继承问题，及创建的线程类为同一对象，可以实现线程共享同一内存
* 不管是单继承还实现接口方式，数据的同步(synchronized)需要通过锁机制来完成

### 线程间的通信
>通过锁机制、wait()与notify()、join()等方法实现线程间的通信

* yield()方法让出当前占用的cpu，让其他线程执行。但是不会释放其拥有的锁
* wait()方法释放其拥有的锁并处于等待状态，当另一线程调用notify或notifyAll方法时，唤醒wait的线程，并且要获取到锁之后才能进入到可运行状态
* join()方法指的是调用某线程的join方法，该线程执行完毕后，当前线程在继续执行。比如main(){t.join()},t线程执行完毕后，在执行主线程main
* sleep()方法线程睡眠并不释放锁，到达指定时间后处于Runnable状态，等待cpu调度

* 参照：http://www.cnblogs.com/mengdd/archive/2013/02/16/2913628.html

### 线程的状态图
* http://blog.csdn.net/huang_xw/article/details/7316354




