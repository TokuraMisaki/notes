+ 公平lock()
``` java
	// reentrantlock公平锁流程 调用sync.lock()-->公平锁的lock()
	final void lock() {  
	 acquire(1);  
	}
	// 最终调用acquire(1)
	public final void acquire(int arg) {
        if (!tryAcquire(arg) &&
            acquireQueued(addWaiter(Node.EXCLUSIVE), arg))
            selfInterrupt();
    	} 
	}
// 下面对acquire方法进行解析

	protected final boolean tryAcquire(int acquires) {
        // tryAcquire 首先获得当前线程和锁的状态 
            final Thread current = Thread.currentThread();
            int c = getState();
        // 如果锁状态==0 第一次尝试获得锁
            if (c == 0) {
                // 判断是否需要排队 如果不需要 直接CAS获得锁并设置当然持有锁的线程
                // 如果需要进行下一步
                if (!hasQueuedPredecessors() &&
                    compareAndSetState(0, acquires)) {
                    setExclusiveOwnerThread(current);
                    return true;
                }
            }
        // 否则判断是否是重入状态 如果是则锁状态+1 否则返回获得锁失败
            else if (current == getExclusiveOwnerThread()) {
                int nextc = c + acquires;
                if (nextc < 0)
                    throw new Error("Maximum lock count exceeded");
                setState(nextc);
                return true;
            }
            return false;
        }
// 判断是否需要排队
// 第一个线程来争夺锁资源时 tail head都为null
    public final boolean hasQueuedPredecessors() {
        // The correctness of this depends on head being initialized
        // before tail and on head.next being accurate if the current
        // thread is first in queue.
        Node t = tail; // Read fields in reverse initialization order
        Node h = head;
        Node s;
        return h != t &&
            ((s = h.next) == null || s.thread != Thread.currentThread());
    }
```

