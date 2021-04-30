Multi threading
=================


Multithreading in java is a process of executing multiple threads simultaneously. Thread is basically a lightweight sub-process, a smallest unit of processing. Multiprocessing and multithreading, both are used to achieve multitasking.

But we use multithreading than multiprocessing because threads share a common memory area. They don't allocate separate memory area so saves memory, and context-switching between the threads takes less time than process.

Thread is executed inside the process. There is context-switching between the threads. There can be multiple processes inside the OS and one process can have multiple threads.


Advantages of Multithreading:
-------------------

1. It doesn't block the user because threads are independent and you can perform multiple operations at same time.
2. You can perform many operations simultaneously so it saves time.
3. Threads are independent so it doesn't affect other threads if exception occur in a single thread.


Life Cycle of a Thread
-----------------------
A java thread can be in any of following thread states during it’s life cycle i.e. New, Runnable, Blocked, Waiting, Timed Waiting or Terminated. These are also called life cycle events of a thread in java.

- **New** - The thread is in new state if you create an instance of Thread class but before the invocation of start() method.
- **Runnable** - The thread is in runnable state after invocation of start() method, but the thread scheduler has not selected it to be the running thread.
- **Running** - The thread is in running state if the thread scheduler has selected it.
- **Non-Runnable (Blocked)** - This is the state when the thread is still alive, but is currently not eligible to run.
- **Terminated** - A thread is in terminated or dead state when its run() method exits.


 <img src="../images/Life-Cycle-Thread.png" width="700" border="2" />



Creating a Thread
-----------------
There are two ways to create a thread:
1. extends Thread class
2. implement Runnable interface



- **Extends Thread class**
  Create a thread by a new class that extends Thread class and create an instance of that class. The extending class must override run() method which is the entry point of new thread.

```java
public class MyThread extends Thread {

    public void run() {
      System.out.println("Thread started running..");
    }
    public static void main( String args[] ) {
       MyThread mt = new  MyThread();
       mt.start();
    }
}

```
Output
```html
Thread started running..
```
- **Implementing the Runnable Interface**

After implementing runnable interface, the class needs to implement the run() method, which is public void run().

- run() method introduces a concurrent thread into your program. This thread will end when run() returns.
- You must specify the code for your thread inside run() method.
- run() method can call other methods, can use other classes and declare variables just like any other normal method.

```java
class MyThread implements Runnable {

    public void run() {
        System.out.println("Thread started running..");
    }
    public static void main(String args[]) {
        MyThread mt = new MyThread();
        Thread t = new Thread(mt);
        t.start();
    }
}
```

- **Difference between Runnable vs Thread**

- Implementing Runnable is the preferred way to do it. Here, you’re not really specializing or modifying the thread’s behavior. You’re just giving the thread something to run. That means composition is the better way to go.
- Java only supports single inheritance, so you can only extend one class.
- Instantiating an interface gives a cleaner separation between your code and the implementation of threads.
- Implementing Runnable makes your class more flexible. If you extend Thread then the action you’re doing is always going to be in a thread. However, if you implement Runnable it doesn’t have to be. You can run it in a thread, or pass it to some kind of executor service, or just pass it around as a task within a single threaded application.

A thread can be defined in two ways. First, by extending a **Thread class** that has already implemented a Runnable interface. Second, by directly implementing a **Runnable interface**.

**Difference**

|THREAD	CLASS                               |RUNNABLE INTERFACE                                             |
|-------------------------------------------|---------------------------------------------------------------|
|Each thread creates a unique object and gets associated with it.|	Multiple threads share the same objects.|
|As each thread create a unique object, more memory required.|As multiple threads share the same object less memory is used.|
|In Java, multiple inheritance not allowed hence, after a class extends Thread class, it can not extend any other class.|	If a class define thread implementing the Runnable interface it has a chance of extending one class.|
|A user must extend thread class only if it wants to override the other methods in Thread class.|If you only want to specialize run method then implementing Runnable is a better option.|
|Extending Thread class introduces tight coupling as the class contains code of Thread class and also the job assigned to the thread|	Implementing Runnable interface introduces loose coupling as the code of Thread is separate form the job of Threads.|


## Q. What does join() method?

`java.lang.Thread` class provides the join() method which allows one thread to wait until another thread completes its execution.
```java
public class ThreadJoinExample {

    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable(), "t1");
        Thread t2 = new Thread(new MyRunnable(), "t2");
        Thread t3 = new Thread(new MyRunnable(), "t3");
        
        t1.start();
        
        //start second thread after waiting for 2 seconds or if it's dead
        try {
            t1.join(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        t2.start();
        
        //start third thread only when first thread is dead
        try {
            t1.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        t3.start();
        
        //let all threads finish execution before finishing main thread
        try {
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        
        System.out.println("All threads are dead, exiting main thread");
    }

}

class MyRunnable implements Runnable {

    @Override
    public void run() {
        System.out.println("Thread started: "+Thread.currentThread().getName());
        try {
            Thread.sleep(4000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("Thread ended: "+Thread.currentThread().getName());
    }
}
```
Output
```
Thread started: t1
Thread started: t2
Thread ended: t1
Thread started: t3
Thread ended: t2
Thread ended: t3
All threads are dead, exiting main thread
```
<div align="right">
    <b><a href="#">↥ back to top</a></b>
</div>



You have thread T1, T2, and T3, how will you ensure that thread T2 run after T1 and thread T3 run after T2?

For more information:
1. [How to join two threads in Java? Thread.join()](https://www.java67.com/2015/07/how-to-join-two-threads-in-java-example.html)
2. [Multithreading Interview Questions and Answers](https://github.com/learning-zone/java-interview-questions/blob/master/multithreading-questions.md)

    





