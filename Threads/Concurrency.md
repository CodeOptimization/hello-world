# The many faces of concurrency
## Faster execution
  The problems that you solve with concurrency can be roughly classfied as "speed" and "design manageaability".
1. In face, from the performance standpoint , it makes no sense to use concurrency on a single processor machine unless one of the 
  tasks mightblock.
  
2. By creating a separate thread of execution to respond to user input, even though the thread will be blocked most of the time, the 
  programm guarantees a certain level of responsiveness.
  
3. Since there are generally quantity and overhead limitations to processes that prevent using processes to concurrency.
  
4. Java took more traditional approach to adding supporting for threading on top of a sequential language, Instead of forking external processes in a multitasking OS, threading creates tasks with a process represented by the executing program. Another compelling reason is to import cucurrency into single-process OS.
