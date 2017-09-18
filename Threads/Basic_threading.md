# Basic threading

1. A thread is a single unique sequential flow of control within a process.

2. A single process thus can have multiple cuncurrently executing tasks, but your program as of each task has the CPU to itself.

3. Threading is a way to create transparently scalable programs -- if a program is running too slow, you can easily speed it up by adding CPUs to the server.

## Defining tasks

4. A thread drives a task, so you need a way to describe that task. This is provided by the Runnable interface. To define a task, simply 
implement Runnable and write a run() method to make the task do your bidding.

5. A task's run() method usually has some kind of loop that continues until the task is no longer necessary, so you must establish the condition on which to break out of this loop.

6. To establish a thread either __(1)__ implement the Runnable interface and call the run() method, or __(2)__ hand the Runnable object to a Thread constructor.

7. Even coding like "new Thread(new RunnableClass())" instead of "Thread t = new Thread(new RunnableClass())" does not make it fair game for garbage collector. Because, each Thread "registers" itself so there is actually a reference to it someplace ana garbage collector can't clean it up until the task exits its run() and dies.

## Usign Exeutors

8. Executors allow you to run manage the execution of asynchronous tasks without having to explicitly manage the ilfecycle of threads.

9. CachedThreadPool: create one thread per task, create as many as it needs; FixedThreadPool: uses a limited set of threads to execute the submitted tasks.

10. Characters of FixedThreadPool: expenive to init; event driven; bounded number of threads to prevent overusing resources; automatically resued. A SingleThreadExecutor is like a FixedThreadExecutor with fixed number as 1.
