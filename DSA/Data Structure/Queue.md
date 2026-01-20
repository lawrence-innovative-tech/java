#### **Queue
- Data structure is using (FIFO) First in First Out. Insertion at end (Enqueue), remove or read at first (dequeue) technics.
- Queue is not synchronized, if needs synchronous use Blocking queues.
- queue uses Two pointer technique to locate their current position, left and right.
- Linked list implements dequeue interface.
#### **Type of Queues
1. Simple or Regular queue
2. Circular Queue
3. Dequeue (Top - End queue)
4. Priority Queue
5. Blocking queue (for concurrency)

#### **Simple or Regular queue
- Normal queue above declares it's definition, but it have drawback,
	- Above [[#**Queue|queue]] definition describe normal queue.
	- Here, queue has one drawback, when last index or position reached, if previous space are available it never allows to insert. So, they designed [[#**Circular Queue|circular queue]].
#### **Circular Queue
- Circular queue also working the same principle above mentioned. But the above drawback are solved here using Module operator.
	- E.x. index - \[right + 1] % size.
- It get wrap around.
- No wasted space, wrap around.

#### **Dequeue (Top - End queue)
- 