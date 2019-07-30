# Deadlock problem

A **deadlock** happens when two threads each wait for a resource held by the other, so neither can proceed.

For example, might innocently lock private field a within your class x, unaware that your caller \(or caller's caller\) has already locked field b within class y. Meanwhile, another thread is doing the reverse — creating a deadlock. Ironically, the problem is exacerbated by \(good\) object-oriented design patterns, because such patterns create call chains that are not determined until runtime.

The popular advice, “lock objects in a consistent order to avoid deadlocks,” although helpful in our initial example, is hard to apply to the scenario just described. A better strategy is to be wary of locking around calling methods in objects that may have references back to your own object. Also, consider whether you really need to lock around calling methods in other classes \(often you do — [as we’ll see later](http://www.albahari.com/threading/part2.aspx#_Locking) — but sometimes there are other options\). Relying more on [declarative](http://www.albahari.com/threading/part5.aspx#_PLINQ) and [data parallelism](http://www.albahari.com/threading/part5.aspx#_The_Parallel_Class), [immutable types](http://www.albahari.com/threading/part2.aspx#_Immutable_Objects), and [nonblocking synchronization constructs](http://www.albahari.com/threading/part4.aspx#_Nonblocking_Synchronization), can lessen the need for locking.

