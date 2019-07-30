# Understand differences between Concurrency vs Multi-threading vs Asynchronous

  
**Single Threaded** – If we have couple of tasks to be worked on and the current system provides just a single thread, then tasks are assigned to the thread one by one.

![](../../.gitbook/assets/image%20%28113%29.png)

**Multi-Threaded** – In this environment, we used to have multiple threads which can take up these tasks and start working on that.

![](../../.gitbook/assets/image%20%2871%29.png)

**Asynchronous** Programming Model – In contrary to Synchronous programming model, here a thread once start executing a task it can hold it in mid, save the current state and start executing another task.

![](../../.gitbook/assets/image%20%2860%29.png)

If our system is capable of having multiple threads then all the threads can work in asynchronous model as well

![](../../.gitbook/assets/image%20%28133%29.png)

**Concurrency** means processing multiple requests at a time. There are two scenarios where multiple requests were getting processed, Multi-threaded programming and asynchronous model.

