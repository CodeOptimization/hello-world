# The many faces of concurrency
1. Faster execution
  1.1 In face, from the performance standpoint , it makes no sense to use concurrency on a single processor machine unless one of the 
  tasks mightblock.
  1.2 By creating a separate thread of execution to respond to user input, even though the thread will be blocked most of the time, the 
  programm guarantees a certain level of responsiveness.
  1.3 Since there are generally quantity and overhead limitations to processes that prevent using processes to concurrency.
  1.4 Java took more traditional approach to adding supporting for threading on top of a sequential language, Instead of forking external 
  processes in a multitasking OS, threading creates tasks with a process represented by the executing program. Another compelling reason 
  is to import cucurrency into single-process OS.