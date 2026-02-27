
#### **Sealed class
- Sealed class are restrict inheritance to any class can inherit. before every class can inherit from other classes. now developer can restrict and permits which subclass can inherit or not.
- Sealed class only allowed only permitted subclasses or interfaces. and subclasses should in following,
	1. final - no further class inherit this subclass.
	2. sealed - the subclass can decided only permitted subclass of subclasses.
	3. non-sealed - normal open to all any class can inherit without restriction.
#### **Records
- Records is immutable data transfer object.
- No other records or class are extends because by default Records extends java.lang.Records. And it a final class no class inherit from this class, and no class other class extends this class. Only interface can implement.
- Records suitable for DTO, Request and response, projection, manages data. But not suitable for Entity (because entity has access to rewrite fetched data, but record are final so initialization at the beginning or constructor), Extended type dto.
- Records are perform Serialization and deserialization.
