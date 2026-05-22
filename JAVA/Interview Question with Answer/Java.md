1. **String constant pool and why String is mutable?**
	- Memory Efficiency -> more string can occur easily so, java design SCP for storing string. String literal directly stores SCP. new String creates forces to create object heap and heap points to SCP. That'swhy heap object intern() method reference comparison become true. 
	- Thread safe, mutable content read-only so multiple thread multiple times read only same content.
	- Hashcode generation, By default hash code generates by memory address + timestamp. String overrides hashCode and equals methods based on value. If it immutable everytime to generate hashcode but it one time generated and use it.
	- Security, when Memory efficient handles one more variable pointing same reference in SCP. if one can change values it automatically others get updated.

2. **A class have 100 fields but only 50 field should serializable ? How can you achieve?
	- If result in json serialization, can use @JsonIgnore or @JsonIgnoreProperties because Jackson uses reflection for serialization.
	- Or Explicitly handles using reflection. \----- but not sure. implicitly
	
3. **What is Stereo type springboot ?
	- Web / Rest layer, service layer, data layer represented @RestController, @Controller, @Service, @Repository but, all are inside using @Component annotation.
4. [[Object Class#**Covariant|Covariant]]
5. **2PC ->** 2 phase commit, Prepare request for all the participants and sent request each participants perform and lock their transactions, and waiting for all the service to respond back success or failure. if success send commit instruction to all the participants, if failed rollback.
6. **Saga pattern ->** Choreography, Orchestration | saga pattern rollback means, compensation transaction, it handles by business level not db rollback level.
	1. Choreography - Eventual consistency, Service to service communicates eventual each service perform their action, performance success pass to next step if failed pass event to previous unstill start transaction to rollback.
	2. Orchestration - Central control transaction, Central engine decide to to next or rollback to previous stage.
7. **Transaction Outbox pattern ->** Atomicity, transaction is cross functionality guarantee transaction management.
	1. The action with outbox table for track, kafka messages guarantee process with idempotency because kafka published event according to commitment. 
	2. e.x when one action success, system require process two or more cross functional action with guarantee, Like when, order has been placed system perform both inventory service to produce message and assign delivery partner to assign. if one filed rollback the transaction.
	3. database side normal rollback operation to rollback if co works failed.
