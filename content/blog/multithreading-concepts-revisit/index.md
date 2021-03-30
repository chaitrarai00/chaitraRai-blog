---
title: Multithreading revisit
date: "2021-03-30T23:46:37.121Z"
description: "Lets just have a look into multithreading when u walk by!"
---

Creating threads:
One can create threads extending Thread or implementing runnable. Both has the method void run() for operating thread operations. Now assuming that we want our run to return a value the this isn’t possible with thread and runnable. That’s why there is a Callable<T> Interface. And method T call().

In ExecutorService where we submit task the submit which accepts the callable object which returns a value of Type<T>. the execute method of ExecutorService exepcts a runnable object hence for a callable object it uses the submit() method and to store it in the variable of type Future<T>.

```java
int corecount=Runtime.getRuntime.availableProcessors();
ExecutorService service=Executors.newFixedThreadPool(corecount);
for(int i=0;i<1000;i++){
	Future<Integer> future=service.submit(new Task()); //Task implements Callable<Integer>
}
```

Volatile vs atomic
![thread1visibilityproblem](./thread1visibilityproblem.png)
Here thread1 and thread2 are run together but the variable might not change due to the Visibility problem where thread1 and thread 2 do not reflect changes as they are not aware of the changes undergone in the cache.
The reason underlies in the way the memory is structured.
![thread1visibilityproblemreasonstructure](./thread1visibilityproblemreasonstructure.png)

Here we see the variable values do not reflect the changes from cache unless we declare the variable as volatile where we actually indiacate that the variable has to impact the memory and pick changes from there rather than the local cache.
![thread1visibilityproblemsolutionvolatile](./thread1visibilityproblemsolutionvolatile.png)
The next problem lies when we have the synchronization problem for any compound operations.
![threadsynchronizationcompoundproblem](./threadsynchronizationcompoundproblem.png)
Consider this example where value is being incremented by 2 threads we would want it to be synchronously behaving but this will based on our processors behave like so
• first change value to 2 by thread 1
• again thread 2 would change value to 2 from 1 since it doesn’t know that thread 1 has changed the value prior to this
To solve this one can approach 2 solutions 1 the AtomicInteger or synchronize the blocks.
![threadsynchronizationcompoundproblematomic](./threadsynchronizationcompoundproblematomic.png)
![threadsynchronizationcompoundproblematomic](./threadsynchronizationcompoundproblematomic.png)

ThreadLocal: It guarantees to maintain thread confinement among large number of threads, and ensures the context comes or communicates among all threads created without the issue of synchronization by assigning one object per thread and also creating minimum number of objects
Eg: public static ThreadLocal<T> holder=new ThreadLocal();
usecases: LocaleContextHolder,SecurityContextHolder,DatatimeContextHolder etc

In Java one can achieve parallelism provided the cpu had more than 1 core( dual core having 2 threads to run in parallel, 3 cores run 3 thread in parallel and so on)
We can achieve parallelism by simply running custom thread or by creating thread pools(ExecutorService, ForkJoinPool, Custom ThreadPools(in webservers)
Concurrencyy occurs when multiple threads might have to access or update or both a shared resource or may be multiple tasks have to be coordinate together. Java offers multiple ways to achieve this like locks/synchronized, Atomic classes, Concurrent Datastructure(concurrentHashmap, BlockingQueue), CompletableFuture, Countdown Latch/ CyclicBarrier/Semaphore/Phaser

ExecutorService:
Instead of creating n number of threads for n tasks (say n=1000) which would be costly we would work on creating m number of threads(say m= 10) and take up 1000 tasks by these 10 threads and just execute to let the thread puck up tasks.

```java
ExecutorService service=Executors.newFixedThreadPool(10);
for(int i=0;i<1000;i++){
	service.execute(new Task());
//here the threads in pool of 10 will pick up tasks themselves
}
```

Threadpool internally keeps a blocking queue which handles concurrent operations and the threads all together does the fetching of new task executing it and returning back, once task is completed fetch another task.
Ideal pool size depends on the tasks involved. A I/O intensive operations will need a large number of threads so that even if some threads go to wait remaining threads can pick up new tasks. A CPU intensive operation might give good performance based on number of cores/ OS threads possible.

```java
int corecount=Runtime.getRuntime.availableProcessors();
ExecutorService service=Executors.newFixedThreadPool(corecount);
for(int i=0;i<1000;i++){
	service.execute(new Task());
}
```

ExecutorService:
• fixed Thread Pool: fixed number of threads, blockingqueue that holds the tasks
• cached thread pool: no fixed number of threads it has a synchronous queue. When a task is created the task is pushed into the synchronous queue and the queue find the thread that is free to take up the task and then assigns the task to this thread. And if any thread is not free then we create a new thread,add to pool and assign the task accordingly. If the thread is idle for 60 seconds its killed.
• Scheduled Thread Pool: taks that has to be executed with fixed delay or fixed rate. The queue is a delay queue and here the tasks are distributed based on when it has to be executed and might not be sequential based on the way you insert the task. Threads will be created if needed.
• Single Threaded Executor: same as fixed Thread Pool but with one single thread. On execption a new thread is recreated when its killed. This is used when u want a task n to be executed before a task n+1 and so on. This can be ensured only with single thread.

References: https://www.youtube.com/channel/UCiz26UeGvcTy4_M3Zhgk7FQ
