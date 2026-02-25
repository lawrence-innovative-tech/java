 #### **Purpose
 - Object class is parent class of all the classes which user creates or build-in. So, it help to generics.
 - Object class provides necessary thinks of the each class. like getClass() to access current object.
 - Reflection, serialization and Threads are access via object class.
 - Object header layout 8-byte (64- Hotspot vm, compressedOops + compressedClassPointer).
 - getClass() method is native final method can't overridden, getClass() calls native method get klass pointer, and communicate to Class object which is present in heap memory.
 - By default hava must extends only one class at a time, so if custom or build-in class extends some other classes jvm automatically writes object extension of parent class.
 - Delegation of lifecycle - B -> A -> object class.

#### **Object class methods
1. hashcode - by default it generate hash of memory it can overrides it will generate based on that.
2. equlas - by default it will checks references, when the class overrides checks based on overriden.
3. toString - by default it will print classname + hashcode of object, based on overriden it will print.
4. notify -
5. notifyall -
6. wait -
7. finalize - when object will destroy gc calls finalize method but now it deprecated, this clear the used value of that object.

Your understanding was correct on every major point:

- HashCode first → mixing (xor inside fingerprint) → mask with (n-1) → bucket.
- Inside bucket: quick hash match → then equals check (custom or default).
- When equals is true → override the value (“override the content”).
- When equals is false → just add as another resident in the same bucket.

#### **Purpose of HashCode & equals
- Actually, Hash based collection buckets allocation will occur Collision, because if two object have same content but both are different hashcode hashmap allocates different buckets.
- But it may same person creates two times of object with same content java treats as different person, different content is collision, logically failed.
- If it override content and checks whether both have same content or not. if it both meets same it should allocates same buckets or it should be overrides.
- But, by default hashmap checks initially hashcode, if already buckets have values checks whether where both content are same using equals method. if same overrides or add new or consider new records. so when equals and hashcode both usage is powerful.

#### **HashCode
- By default, object creates it's generate unique hash for memory (Mark down) + memory address. but if it will overrides will creates new hash.

#### **Equals 
- By default, it will check reference both are same or not.