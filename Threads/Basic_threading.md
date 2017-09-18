# Basic threading

1. A thread is a single unique sequential flow of control within a process.

2. A single process thus can have multiple cuncurrently executing tasks, but your program as of each task has the CPU to itself.

3. Threading is a way to create transparently scalable programs -- if a program is running too slow, you can easily speed it up by adding CPUs to the server.

## Defining tasks

4. A thread drives a task, so you need a way to describe that task. This is provided by the Runnable interface. To define a task, simply 
implement Runnable and write a run() method to make the task do your bidding.

5. A task's run() method usually has some kind of loop that continues until the task is no longer necessary, so you must establish the condition on which to break out of this loop.

6. To establish a thread either __(1)__ implementing the Runnable interface and call the run() method, or hand the Runnable object to a Thread constructor or a ExecutorService;  __(2)__ extending the __Thread__ class.

7. Even coding like "new Thread(new RunnableClass())" instead of "Thread t = new Thread(new RunnableClass())" does not make it fair game for garbage collector. Because, each Thread "registers" itself so there is actually a reference to it someplace ana garbage collector can't clean it up until the task exits its run() and dies.

## Using Exeutors

8. Executors allow you to run manage the execution of asynchronous tasks without having to explicitly manage the ilfecycle of threads.

9. CachedThreadPool: create one thread per task, create as many as it needs; FixedThreadPool: uses a limited set of threads to execute the submitted tasks.

10. Characters of FixedThreadPool: expenive to init; event driven; bounded number of threads to prevent overusing resources; automatically resued. A SingleThreadExecutor is like a FixedThreadExecutor with fixed number as 1.

11. If you have many threads and a easier way to keep synchronizing is using SingleThreadExecutor, each task will serialize the tasks that are submitted to it and maintain its own queue of pending tasks.

## Producing a return value from tasks

12. A Runnable is a seperate task that performs work, but it does't return a value. And a Callable interface object, a generic with a type parameter representing the return value from the method call(), will do the job. The call() method must be invoked by the ExecutorService __submit()__ method.

13. The __submit()__ method produces a __Future__ object, parametered from the particular return type of result returned by the __Callable__.

14. A Future object will get the result by __get()__ method and it will be blocked until __Callable__ object complete execution. (P1124)

## Sleeping

15. __sleep()__ is a way to cease(block) the execution of certain task for a given time.

## Yielding

16. When you've accomplished what you need to during onw pass through a loop in your __run()__ method, you can give a hint(not guaranteed) to the thread-scheduling mechanism that you've done enough by calling __yield()__.

## Daemon thread

17. A daemon thread is intended to provide a genaral service in the background as long as the program is running, but is not part of the essence of the program. You can set one thread as daemon by calling __setDaemon()__. And to check __isDeamon()__.

18. Deamon threads will be generated inside a daemon thread's __run()__ method.

19. __Daemon__ threads will terminate their __run()__ methods without executing __finally__ clauses.

## Code variations

20. Inheriting the __Thread__ class is also a way to implementing tasks.

21. Starting threads inside a constructor could be probelematic, because another task might start executing before constructor has completedm, which means the rask may be able to access the object in a unsafe state.

## Terminology

22. Task vs Thread: Task is more focusing on the woek that is being done and Thread is referring to the specific mechanism that's driving the task.

## Joining a thread

23. 




