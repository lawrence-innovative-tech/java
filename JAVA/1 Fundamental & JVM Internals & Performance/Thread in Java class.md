#### **Requisites 
- [[Memory Model#**Thread Mechanism|Introduction part]]
#### **Purpose
- Each thread handles individual stack to tracks method calling, returns, method parameters. But, Heap object is shared, when multiple thread can access the same resources or heap object **Race condition** occurs. While multi thread can access the same resources read only never meets problems instead if, update or count or like process become cause. If, possible to both thread can read input and update same output, but the output should in continues.
- ex, 
- ```java
  
  class IntrinsicThreadFailedMechanism implement Runnable {
		  int count = 5;

		  @Override
		  public void run(){
			  count += 1;
		  }
		  IntrinsicThreadFailedMechanism itfm = new IntrinsicThreadFailedMechanism();
		    Thread t1 = new Thread(itfm);
		    t1.start();
		    Thread t2 = new Thread(itfm);
		    t2.start();
			
  }
  
  Ouput :
  Thread t1 - 6
  Thread t2 - 6
  
  This Race condition no lock but shard resource can cause this problems.
  Intrinsic is overcome this problem.
  
  ```

#### **Thread lifecycle & Internal flow
- **New State -** When thread creation, it allocates memory in heap, with fields.
- **Runnable -** When thread start(), Jvm calls os to create native thread and allocates stack of that thread, creates TLS (Thread local storage) for get thread info in every time with unique and thread can shared this each. PC counter creates and sta

