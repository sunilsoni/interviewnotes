Multi threading
=================


Multithreading in java is a process of executing multiple threads simultaneously. Thread is basically a lightweight sub-process, a smallest unit of processing. Multiprocessing and multithreading, both are used to achieve multitasking.

But we use multithreading than multiprocessing because threads share a common memory area. They don't allocate separate memory area so saves memory, and context-switching between the threads takes less time than process.

Thread is executed inside the process. There is context-switching between the threads. There can be multiple processes inside the OS and one process can have multiple threads.


Advantages of Multithreading:
-------------------


It doesn't block the user because threads are independent and you can perform multiple operations at same time.
You can perform many operations simultaneously so it saves time.
Threads are independent so it doesn't affect other threads if exception occur in a single thread.


Life Cycle of a Thread
----------
The life cycle of the thread in java is controlled by JVM. The java thread states are as follows:

- **New** - The thread is in new state if you create an instance of Thread class but before the invocation of start() method.
- **Runnable** - The thread is in runnable state after invocation of start() method, but the thread scheduler has not selected it to be the running thread.
- **Running** - The thread is in running state if the thread scheduler has selected it.
- **Non-Runnable (Blocked)** - This is the state when the thread is still alive, but is currently not eligible to run.
- **Terminated** - A thread is in terminated or dead state when its run() method exits.


 <img src="././images/Life-Cycle-Thread.png" width="700" border="2" />



Creating a Thread
-----------------




You have thread T1, T2, and T3, how will you ensure that thread T2 run after T1 and thread T3 run after T2?

For more information:
1. [How to join two threads in Java? Thread.join()](https://www.java67.com/2015/07/how-to-join-two-threads-in-java-example.html)







