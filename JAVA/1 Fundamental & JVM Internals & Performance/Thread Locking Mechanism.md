#### **Objective
- Object are shared resource, when multiple thread access same resource it should create multiple causes. Here, occurs race condition to access the memory.
- Both thread can read same value no issues but writing overlap. So, java has several locking strategies.
	1. Intrinsic Lock (using Synchronized)
	2. Re-entrant Lock
	3. ReadWriteLock
	4. StampedLock
#### **Intrinsic Lock
- Lock mechanism handles by jvm. It object level locking. When 
