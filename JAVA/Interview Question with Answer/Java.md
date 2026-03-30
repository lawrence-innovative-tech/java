1. **String content pool and why String is mutable?**
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
5. 