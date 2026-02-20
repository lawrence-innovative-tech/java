 #### **Purpose
 - Object class is parent class of all the classes which user creates or build-in. So, it help to generics.
 - Object class provides necessary thinks of the each class. like getClass() to access current object.
 - Reflection, serialization and Threads are access via object class.
 - Object header layout 8-byte (64- Hotspot vm, compressedOops + compressedClassPointer).
 - getClass() method is native final method can't overridden, getClass() calls native method get klass pointer, and communicate to Class object which is present in heap memory.

Your understanding was correct on every major point:

- HashCode first → mixing (xor inside fingerprint) → mask with (n-1) → bucket.
- Inside bucket: quick hash match → then equals check (custom or default).
- When equals is true → override the value (“override the content”).
- When equals is false → just add as another resident in the same bucket.