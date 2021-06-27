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
1. Extends Thread class
2. Implement Runnable interface



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

synchronized keyword
----------
`synchronized` keyword in java is used to control the access of multiple threads to any shared resource, so that any consistency problem can be avoided.
We can make the entire method as `synchronized` or just the part where the shared resource is getting used, to do this `synchronized` blocks are used.

Synchronized method/block can only have one thread executing inside it, all the other threads trying to enter into the `synchronized` method/block will get blocked until the thread inside finishes its execution. When the thread exits the `synchronized` method/block then Java guarantees that changes to the state of the object is visible to all the threads. This eliminates the memory inconsistency errors.

static synchronization
----------
When synchronized keyword is used with a static method, then that is called static synchronization. In this, lock will be on the class not the object. This means only one thread can access the class at a time.

The purpose of static synchronization is to make the static data thread-safe.

Let’s look at some programs:

Here, we have a Hello class which has a synchronized method:
```java
class Hello {

	synchronized void sayHello() {
		System.out.println("in sayHello() method " + Thread.currentThread().getName());
		for(int i=1; i<=5; i++) {
			System.out.println(Thread.currentThread().getName() + " , i = " + i);
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
}
```

A Task class which implements Runnable and its run() method simply calls the synchronized method of Hello class:
```java
class Task implements Runnable {

	Hello h;
	
	Task(Hello h) {
		this.h = h;
	}
	
	@Override
	public void run() {
		h.sayHello();
	}

}
```
Our main class:
```java
public class SynchronizationDemo {
public static void main(String[] args) {
Hello obj1 = new Hello();
Hello obj2 = new Hello();

		Thread task1 = new Thread(new Task(obj1));
		task1.setName("First Thread");
		Thread task2 = new Thread(new Task(obj1));
		task2.setName("Second Thread");
		Thread task3 = new Thread(new Task(obj2));
		task3.setName("Third Thread");
		Thread task4 = new Thread(new Task(obj2));
		task4.setName("Fourth Thread");
		
		task1.start();
		task2.start();
		task3.start();
		task4.start();
	}
}
```
We have 2 objects of our Hello class, one object is shared among First and Second thread, and one object is shared among Third and Fourth thread, and we are starting these threads.

Output:
```log
in sayHello() method First Thread
in sayHello() method Third Thread
First Thread , i = 1
Third Thread , i = 1
First Thread , i = 2
Third Thread , i = 2
First Thread , i = 3
Third Thread , i = 3
First Thread , i = 4
Third Thread , i = 4
First Thread , i = 5
Third Thread , i = 5
in sayHello() method Second Thread
Second Thread , i = 1
in sayHello() method Fourth Thread
Fourth Thread , i = 1
Second Thread , i = 2
Fourth Thread , i = 2
Second Thread , i = 3
Fourth Thread , i = 3
Second Thread , i = 4
Fourth Thread , i = 4
Second Thread , i = 5
Fourth Thread , i = 5
```

As you can see from the output, the First and Second thread are not having any thread interference. Same way, Third and Fourth thread does not have any thread interference but First and Third thread are entering the synchronized method at the same time with their own object locks (Hello obj1 and obj2).

Lock which is hold by First thread will only stop the Second thread from entering the synchronized block, because they are working on the same instance i.e. obj1, but it cannot stop Third or Fourth thread as they are working on another instance i.e. obj2.

If we want our synchronized method to be accessed by only one thread at a time then we have to use a static synchronized method/block to have the synchronization on the class level rather than on the instance level.

```java
class Hello {

	static synchronized void sayHello() {
		System.out.println("in sayHello() method " +
									Thread.currentThread().getName());
		for(int i=1; i<=5; i++) {
			System.out.println(Thread.currentThread().getName() + " , i = " + i);
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
}
```

Let’s see the output now:

```log
in sayHello() method First Thread
First Thread , i = 1
First Thread , i = 2
First Thread , i = 3
First Thread , i = 4
First Thread , i = 5
in sayHello() method Fourth Thread
Fourth Thread , i = 1
Fourth Thread , i = 2
Fourth Thread , i = 3
Fourth Thread , i = 4
Fourth Thread , i = 5
in sayHello() method Third Thread
Third Thread , i = 1
Third Thread , i = 2
Third Thread , i = 3
Third Thread , i = 4
Third Thread , i = 5
in sayHello() method Second Thread
Second Thread , i = 1
Second Thread , i = 2
Second Thread , i = 3
Second Thread , i = 4
Second Thread , i = 5
```

Here, only one thread is accessing the static synchronized method.

Same can be done by synchronized block also:
```java
class Hello {

	static void sayHello() {
      synchronized (Hello.class) {
        System.out.println("in sayHello() method " + Thread.currentThread().getName());
        for (int i = 1; i <= 5; i++) {
          System.out.println(Thread.currentThread().getName() + " , i = " + i);
          try {
            Thread.sleep(1000);
          } catch (InterruptedException e) {
            e.printStackTrace();
          }
        }
      }
    }
}
```

## What does join() method?

`java.lang.Thread` class provides the `join()` method which allows one thread to wait until another thread completes its execution. `join()` method can be used to execute the threads sequentially or in some specific order.
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

In the code, if you don’t write t2.join(), then current thread will not wait from the t2 thread to die.

There are overloaded versions of join() method also,
- **join(long milliseconds)** : when this method is called, then the current thread will wait at most for the specified milliseconds
- **join(long milliseconds, long nanoseconds)** : when this method is called, then the current thread will wait at most for the specified milliseconds plus nanoseconds.

These join methods are dependent on the underlying Operating system for timing. So, you should not assume that join() will wait exactly as long as you specify.
You can execute threads in a sequence using CountDownLatch also.


Deadlock
--------
Deadlock is a programming situation where two or more threads are blocked forever, this situation arises with at least two threads and two or more resources.


```java
class HelloClass {
	public synchronized void first(HiClass hi) {
		try {
			Thread.sleep(1000);
		}
		catch(InterruptedException ie) {}
		System.out.println(" HelloClass is calling 	HiClass second() method");
		hi.second();
	}

	public synchronized void second() {
		System.out.println("I am inside second method of HelloClass");
	}
}

class HiClass {
	public synchronized void first(HelloClass he) {
		try {
			Thread.sleep(1000);
		}
		catch(InterruptedException ie){}
		System.out.println(" HiClass is calling HelloClass second() method");
		he.second();
	}

	public synchronized void second() {
		System.out.println("I am inside second method of HiClass");
	}
}

class DeadlockClass extends Thread {
	HelloClass he = new HelloClass();
	HiClass hi = new HiClass();

	public void demo() {
		this.start();
		he.first(hi);
	} 
	public void run() {
		hi.first(he);
	}

	public static void main(String[] args) {
		DeadlockClass dc = new DeadlockClass();
		dc.demo();
	}
}
```

```log
cmd> java DeadlockClass
HelloClass is calling HiClass second() method
HiClass is calling HelloClass second() method
```


How to avoid deadlock?
---------------

- **1. Avoid Nested Locks:**
This is the most common reason for deadlocks, avoid locking another resource if you already hold one. It’s almost impossible to get deadlock situation if you are working with only one object lock. For example, here is the another implementation of run() method without nested lock and program runs successfully without deadlock situation.

```java
public void run() {
        String name = Thread.currentThread().getName();
        System.out.println(name + ' acquiring lock on ' + obj1);
        synchronized (obj1) {
          System.out.println(name + ' acquired lock on ' + obj1);
          work();
        }
        System.out.println(name + ' released lock on ' + obj1);
        System.out.println(name + ' acquiring lock on ' + obj2);
        synchronized (obj2) {
          System.out.println(name + ' acquired lock on ' + obj2);
          work();
        }
        System.out.println(name + ' released lock on ' + obj2);
        System.out.println(name + ' finished execution.');
        }
}
```
- **2. Lock Only What is Required:**
  You should acquire lock only on the resources you have to work on, for example in above program I am locking the complete Object resource but if we are only interested in one of it’s fields, then we should lock only that specific field not complete object.
  
- **3. Avoid waiting indefinitely:**
  You can get deadlock if two threads are waiting for each other to finish indefinitely using thread join. If your thread has to wait for another thread to finish, it’s always best to use join with maximum time you want to wait for thread to finish.

What will happen if I directly call the run() method and not the start() method to execute a thread?
------

if run() method is called directly, then a new thread will not be created instead the code will run on the current thread which is main thread. Calling run() method directly will make it behave as any other normal method call. Only a call to start() method creates separate thread.

Once a thread has been started can it be started again?
------
No. A thread can be started only once in its lifetime. If you try to start a thread which has already been started, an IllegalThreadStateException is thrown, which is a runtime exception. A thread in runnable state or a dead thread cannot be restarted

Why wait, notify and notifyAll methods are defined in the Object class instead of Thread class?
-------
The methods wait, notify and notifyAll are present in the Object class, that means they are available to all class objects, as Object class is the parent of all classes.
- **wait() method** – it tells the current thread to release the lock and go to sleep until some other thread enters the same monitor and calls notify()
- **notify() method** – wakes up the single thread that is waiting on the same object’s monitor
- **notifyAll() method** – wakes up all the threads that called wait() on the same object

if these methods were in Thread class, then thread T1 must know that another thread T2 is waiting for this particular resource, so T2 can be notified by something like T2.notify()

But in java, the object itself is shared among all the threads, so one thread acquires the lock on this object’s monitor, runs the code and while releasing the lock, it calls the notify or notifyAll method on the object itself, so that any other thread which was “waiting on the same object’s monitor will be notified that now the shared resource is available. That is why these methods are defined in the Object class.

Threads have no specific knowledge of each other. They can run asynchronously and are independent. They do not need to know about the status of other threads. They just need to call notify method on an object, so whichever thread is waiting on that resource will be notified.

Let’s consider this with a real-life example:

Suppose there is a petrol pump and it has a single washroom, the key of which is kept at the service desk. This washroom is a shared resource for all. To use this shared resource, the user must acquire the key to the washroom lock. So, the user goes to service desk, acquires the key, opens the door, locks it from the inside and use the facility.

Meanwhile if another user arrives at the petrol pump and wants to use the washroom, he goes to the washroom and found that it is locked. He goes to the service desk and the key is not there because it is with the current user. When the current user finishes, he unlocks the door and returns the key to the service desk. He does not bother about the waiting users. The service desk gives the key to waiting user. If there are more than one user waiting to use the facility, then they must form a queue.

Now, apply this analogy to Java, one user is one thread and the washroom is the shared resource which the threads wish to execute. The key will be synchronized keyword provided by Java through which thread acquires a lock for the code it wants to execute and making other threads wait until the current thread finishes. Java will not be as fair as the service station, because any of the waiting threads may get a chance to acquire the lock, regardless of the order in which the threads came. The only guarantee is that all the waiting threads will get to use the shared resource sooner or later.

In this example, the lock can be acquired on the key object or the service desk and none of them is a thread. These are the objects that decide whether the washroom is locked or not.

Why wait(), notify(), notifyAll() methods must be called from synchronized block?
------------
These methods are used for inter-thread communication. So, a wait() method only makes sense when there is a notify() method also.
If these methods are not called from a synchronized block then

- IllegalMonitorStateException will be thrown
- Race condition can occur

wait() vs sleep() methods
-----

The differences are:
- `wait()` method can only be called from a synchronized context while `sleep()` method can be called without synchronized context
- `wait()` method releases the lock on the object while waiting but `sleep()` method does not release the lock it holds while waiting, it means if the thread is currently in a synchronized block/method then no other thread can enter this block/method
- `wait()` method is used for inter-thread communication while `sleep()` method is used to introduce a pause on execution
-  waiting thread can be waked by calling `notify()` or `notifyAll()`, while sleeping thread will wake up when the specified sleep time is over or the sleeping thread gets interrupted
- `wait()` method is non-static, it gets called on an object on which synchronization block is locked while `sleep()` is a static method, we call this method like Thread.sleep(), that means it always affects the currently executing thread
- `wait()` is normally called when a condition is fulfilled like if the buffer size of queue is full then producer thread will wait, whereas `sleep()` method can be called without a condition

Executor Framework
-------------

With an Executor framework, we only have to implement the Runnable objects and send them to the executor. The executor is responsible for their execution, instantiation, and running with necessary threads. But it goes beyond that and improves performance using a pool of threads. When you send a task to the executor, it tries to use a pooled thread for the execution of this task, to avoid continuous spawning of threads.

Another important advantage of the Executor framework is the Callable interface. It's similar to the Runnable interface, but offers two improvements, which are:
1. The main method of this interface, named call(), may return a result.
2. When you send a Callable object to an executor, you get an object that implements the Future interface. You can use this object to control the status and the result of the Callable object.

**Summary**
- At a low level, we can create a thread in two ways, either by implementing Runnable or by subclassing Thread and overriding the run() method.
- At a high-level, we use Executors, which use thread pools, which in turn use worker threads.
- One type of thread pool is the fixed thread pool, which has a fixed number of threads running. We can also use single-thread pools.
- ExecutorService has methods to execute thread pools that either take a Runnable or Callable task. A Callable returns a result and throws a checked exception.
- The submit() method returns a Future object that represents the result of the task (if the task is a Runnable, null is returned).
- An executor has to be shutdown to close the pool thread with either shutdown() (gracefully) or shutdownNow() (forcefully).
- A deadlock situation occurs when two or more threads are blocked forever, waiting for each other to acquire/release some resource.
- Starvation happens when a thread is constantly waiting for a lock, never able to take it because other threads with higher priority are continually acquiring it.
- A livelock is like a deadlock in the sense that two (or more) threads are blocking each other, but in a livelock, each thread tries to resolve the problem on its own (live) instead of just waiting (dead).
- A race condition is a situation where two threads compete to access or modify the same resource at the same time in a way that causes unexpected results.

High level concurrency features Executor framework
-------------
- ExecutorService Interface
- ScheduledExecutorService Interface
- Future Interface
- Executors newSingleThreadExecutor Method 
- Executors newFixedThreadPool Method 
- Executors newCachedThreadPool Method 
- Executors newScheduledThreadPool Method 

Executor Interface
-------------

An object that executes submitted Runnable tasks. This interface provides a way of decoupling task submission from the mechanics of how each task will be run, including details of thread use, scheduling, etc. An Executor is normally used instead of explicitly creating threads.

For example, rather than invoking `new Thread(new(RunnableTask())).start()` for each of a set of tasks, you might use:

```java
Executor executor = anExecutor;
 executor.execute(new RunnableTask1());
 executor.execute(new RunnableTask2());
        ...
```

ExecutorService Interface
-------------
The `ExecutorService` interface supplements execute with a similar, but more versatile submit method. Like `execute`, `submit` accepts Runnable objects, but also accepts `Callable` objects, which allow the task to return a value. The submit method returns a `Future` object, which is used to retrieve the `Callable` return value and to manage the status of both `Callable` and `Runnable` tasks.

`ExecutorService` also provides methods for submitting large collections of `Callable` objects. 
Finally, `ExecutorService` provides a number of methods for managing the shutdown of the executor. To support an immediate shutdown, tasks should handle interrupts correctly.

Source Code from JDK Library
```java
public interface ExecutorService extends Executor {

    void shutdown();

    List<Runnable> shutdownNow();

    boolean isShutdown();

    boolean isTerminated();

    boolean awaitTermination(long timeout, TimeUnit unit)
        throws InterruptedException;

    <T> Future<T> submit(Callable<T> task);

    <T> Future<T> submit(Runnable task, T result);

    Future<?> submit(Runnable task);

    <T> List<Future<T>> invokeAll(Collection<? extends Callable<T>> tasks)
        throws InterruptedException;

    <T> List<Future<T>> invokeAll(Collection<? extends Callable<T>> tasks,
                                  long timeout, TimeUnit unit)
        throws InterruptedException;
    <T> T invokeAny(Collection<? extends Callable<T>> tasks)
        throws InterruptedException, ExecutionException;

    <T> T invokeAny(Collection<? extends Callable<T>> tasks,
                    long timeout, TimeUnit unit)
        throws InterruptedException, ExecutionException, TimeoutException;
}
```

ExecutorService Interface Examples
-------------

By  using Executors.newSingleThreadExecutor() method to create an ExecutorService that uses a single worker thread for executing tasks.

```java
public class ExecutorServiceExample {
    public static void main(String[] args) {

        System.out.println("Thread main started");
  
       // Create a task
        Runnable task = () -> {
             for (int i = 0; i < 5; i++) {
                 System.out.println("[" + Thread.currentThread().getName() + "] " + "Message " + i);
             }
        };

        ExecutorService executorService = Executors.newSingleThreadExecutor();

        executorService.execute(task);

        executorService.shutdown();

        System.out.println("Thread main finished");

     }
}
```

```log
Thread main started
Thread main finished
[pool-1-thread-1] Message 0
[pool-1-thread-1] Message 1
[pool-1-thread-1] Message 2
[pool-1-thread-1] Message 3
[pool-1-thread-1] Message 4
```

Different Between execute() and submit() Methods
-------------
- The main difference is submit() method returns Future object for tracking the results but execute() method does't return anthing.
- Both submit() and execute() methods are used to submit a task to Executor framework for asynchronous execution.
- The submit() can accept both Runnable and Callable task but execute() can only accept the Runnable task.
- You can access submit() and execute() from the ExecutorService interface because it also extends the Executor interface which declares the execute() method.

ScheduledExecutorService Interface
-------------
```java

```
Future Interface
-------------
```java

```

Executor Framework-2
-------------
With an Executor framework, we only have to implement the Runnable objects and send them to the executor. The executor is responsible for their execution, instantiation, and running with necessary threads. But it goes beyond that and improves performance using a pool of threads. When you send a task to the executor, it tries to use a pooled thread for the execution of this task, to avoid continuous spawning of threads.

Another important advantage of the Executor framework is the Callable interface. It's similar to the Runnable interface, but offers two improvements, which are as follows:
- **1.** The main method of this interface, named call(), may return a result.
- **2.** When you send a Callable object to an executor, you get an object that implements the Future interface. You can use this object to control the status and the result of the Callable object.

Executor Framework is an abstraction to managing multiple threads by yourself. So, it decouples the execution of a task and the actual task itself. Now, we just have to focus on the task that means, only implement the Runnables and submit them to executor. Then these runnables will be managed by the executor framework. It is available from Java 1.5 onwards.

Also, we don’t have to create new threads every time. With executor framework, we use Thread pools. Think of Thread Pool as a user-defined number of threads which are called worker threads, these are kept alive and reused. The tasks that are submitted to the executor will be executed by these worker threads. If there are more tasks than the threads in the pool, they can be added in a Queue and as soon as one of thread is finished with a task, it can pick the next one from this Queue or else, it will be added back in the pool waiting for a task to be assigned.

So, it saves the overhead of creating a new thread for each task. If you are thinking about what is the problem with creating a new thread every time we want to execute a task, then you should know that creating a thread is an expensive operation. Thread objects use a significant amount of memory, and in a large-scale application, allocating and deallocating many thread objects creates a significant memory management overhead and new threads without any throttling will lead to the creation of large number of threads. These threads will cause wastage of resources.

There are 2 main interfaces that you must know, one is `Executor` and the other is `ExecutorService`.

- **Executor** : interface contains `execute(Runnable task)` method through which you can execute only Runnables. Also, the return type of `execute()` method is void, since you are passing a `Runnable` to it and it does not return any result back.

- **ExecutorService** : interface contains the `submit()` method which can take both `Runnable` and `Callable`, and its return type is Future object. `ExecutorService` extends the `Executor` Interface, so it also has the `execute()` method.

Let’s look at different types of Executors:

- **SingleThreadExecutor** :
  This executor has only one thread and is used to execute tasks in a sequential manner. If the thread dies due to an exception while executing the task, a new thread is created to replace the old thread and the subsequent tasks are executed in the new thread.
  How to create a SingleThreadExecutor:
  
```java
  ExecutorService executor = Executors.newSingleThreadExecutor ();
```
  Executors is a utility class which contains many factory methods to create different types of ExecutorService, like the one called SingleThreadExecutor, we just created.

- **FixedThreadPoolExecutor** :
  As its name suggests, this is an executor with a fixed number of threads. The tasks submitted to this executor are executed by the specified number of threads and if there are more tasks than the number of threads, then those tasks will be added in a queue (e.g. LinkedBlockingQueue).
  How to create a FixedThreadPoolExecutor:
```java
  ExecutorService executor = Executors.newFixedThreadPool (5);
```

 Here, we have created a thread pool executor of 5 threads, that means at any given time, 5 tasks can be managed by this executor. If there are more active tasks, they will be added to a queue until one of the 5 threads becomes free.
  An important advantage of the fixed thread pool is that applications using it degrade gracefully. 
 
 To understand this, consider a web server application where each HTTP request is handled by a separate thread. If the application simply creates a new thread for every new HTTP request, and the system receives more requests than it can handle immediately, the application will suddenly stop responding to all requests when the overhead of all those threads exceed the capacity of the system. With a limit on the number of the threads that can be created, the application will not be servicing HTTP requests as quickly as they come in, but it will be servicing them as quickly as the system can sustain.


- **CachedThreadPoolExecutor** :
  This executor is mainly used when there are many short-lived tasks to be executed. If you compare this with the fixed thread pool, here the number of threads of this executor pool is not bounded. If all the threads are busy executing the assigned tasks and if there is a new task, then a new thread will be created and added to the pool. If a thread remains idle for close to sixty seconds, it is terminated and removed from the cache.
  Use this one, if you are sure that the tasks will be short-lived, otherwise there will be a lot of threads in the pool which will lead to performance issues.
  How to create a CachedThreadPoolExecutor:
```java
  ExecutorService executor = Executors.newCachedThreadPool ();
```

- **ScheduledExecutor** :
  Use this executor, when you want to schedule your tasks, like run them at regular intervals or run them after a given delay. There are 2 methods which are used for scheduling tasks: scheduleAtFixedRate and scheduleWithFixedDelay .
  How to create ScheduledExecutor:

```java
  ExecutorService executor = Executors.newScheduledThreadPool (4);
```
  ScheduledExecutorService interface extends the ExecutorService interface.
  Now, apart from using Executors class to create executors, you can use ThreadPoolExecutor and ScheduledThreadPoolExecutor class also. Using these classes, you can manually configure and fine-tune various parameters of the executor according to your need. 
  
Let’s see at some of those parameters:

```java
  public ThreadPoolExecutor(int corePoolSize,
        int maximumPoolSize,
        long keepAliveTime,
        TimeUnit unit,
        BlockingQueue<Runnable> workQueue,
        ThreadFactory threadFactory,
        RejectedExecutionHandler handler)
```

Core and Max Pool sizes:
> A ThreadPoolExecutor will automatically adjust the pool size according to the bounds set by corePoolSize and maximumPoolSize

When a new task is submitted to the executor then:

- If the number of threads running are less than the corePoolSize, a new thread is created to handle the request
- If the number of threads running are more than corePoolSize but less than maximumPoolSize then a new thread will be created only if the queue is full

Let’s understand this with an example:

You have defined the core pool size as 5, maximum pool size as 10 and the queue capacity as 100. Now as tasks are coming in, new threads will be created up to 5, then other new tasks will be added to queue until it reaches 100. Now when the queue is full and if new tasks are coming in, threads will be created up to the maximumPoolSize i.e. 10. Once all the threads are in use and the queue is also full, the new tasks will be rejected. As the queue reduces, so does the number of active threads.

Keep Alive Time and TimeUnit:
> When the number of threads are greater than the core size, this is the maximum time that excess idle threads will wait for new tasks before terminating. It is used to avoid the overhead of creating a new thread.

Let’s understand this with an example:

You have defined the core pool size as 5 and maximum pool size as 15 and all the 15 threads are getting used at the moment. 

Now when the threads are getting finished with their work, the excess 10 threads (15-5) become idle and eventually die. To avoid these 10 threads being killed too quickly, we can specify the keep alive time for these by using the keepAliveTime parameter in the ThreadPoolExecutor constructor. If you have given its value as 1 and time unit as TimeUnit.MINUTE, each thread will wait for 1 min after it had finished executing a task. Basically, it is waiting for a new task to be assigned. If it is not given any task, it would let itself complete. And in the end, the executor will be left with the core threads (5).

- **BlockingQueue** :
  The queue to use for holding tasks before they are executed. This queue will hold only the Runnable tasks submitted by the execute method, you can use a ArrayBlockingQueue or LinkedBlockingQueue like:
```java  
BlockingQueue<Runnable> queue = new ArrayBlockingQueue<>(100);
```

- **ThreadFactory** :
  The factory to use when the executor creates a new thread. Using thread factories removes hardwiring of calls to new Thread , enabling applications to use special thread subclasses, priorities, etc.
  
- **RejectedExecutionHandler** : 

This handler is used when a task is rejected by the executor because all the threads are busy and the queue is full.

When this handler is not provided and the task submitted to execute() method is rejected, then an unchecked RejectedExecutionException is thrown.
But adding a handler is a good practice to follow, there is a method:
```java  
void rejectedExecution(Runnable r , ThreadPoolExecutor executor );
```

This method will be invoked by ThreadPoolExecutor when execute() cannot accept a task.
Putting it all together:
```java  
BlockingQueue<Runnable> blockingQueue = new ArrayBlockingQueue<Runnable>(50);
        CustomThreadPoolExecutor executor = new CustomThreadPoolExecutor(5,15, 5000, TimeUnit.MILLISECONDS, blockingQueue);
        executor.setRejectedExecutionHandler(new RejectedExecutionHandler() {
            @Override
            public void rejectedExecution(Runnable r, ThreadPoolExecutor executor) {
                System.out.println("Waiting for a second !!");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                executor.execute(r);
            }
        });
```


For more information:
1. [How to join two threads in Java? Thread.join()](https://www.java67.com/2015/07/how-to-join-two-threads-in-java-example.html)
2. [Multithreading Interview Questions and Answers](https://github.com/learning-zone/java-interview-questions/blob/master/multithreading-questions.md)
3. [ExecutorService Interface Overview](https://www.javaguides.net/2018/09/executorservice-interface-in-java.html)

    





