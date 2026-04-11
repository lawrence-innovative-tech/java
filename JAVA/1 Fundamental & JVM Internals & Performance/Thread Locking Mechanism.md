#### **Objective
- Object are shared resource, when multiple thread access same resource it should create multiple causes. Here, occurs race condition to access the memory.
- Both thread can read same value no issues but writing overlap. So, java has several locking strategies.
	1. Intrinsic Lock (using Synchronized)
	2. Re-entrant Lock
	3. ReadWriteLock
	4. StampedLock
#### **Intrinsic Lock
- Lock mechanism handles by jvm. It object level locking. When object enters into synchronized block or method mark thread details in Mark work part which in object header.
- The follower thread never initiate become waiting stage added into waiting stage.

#### **Re-entrant Lock
- Re entrant lock is external locking mechanism, and features to timeout based try lock ().
- When thread locks current object it update count become in one so, followers thread waiting in the queue, the same thread able to lock again and again the same lock but the lock count get increasing. When, thread release the count will reduced it completely done. 
- There are two type of mechanism follower thread decision based on Fair or Unfair,
  Fair process only FIFO mechanism but unfair any active thread become to enters.

#### **Stamped Lock
- Stamp lock contains Read Write lock, optimistic lock but it doesn't allow re entrant lock.
- stamped lock waiting to write all the read thread has complete.

#### **Why thread stamped are not allow to re entrant lock?
- When methods has lock, if it calls to inside the method that methods haven't lock mechanism it possible occur race conditions.
- 