#Abstractions for Common Interface and Types

Clojure provides api for abstractions that may remind you of object oriented programming as you know it from languages such as Java or javascript. However the following distinction is paramount: clojure does not promote the use of objects for representing mutable state, something that object-oriented languages do. If you really want to mirror state inside objects, you can: you may spin off JVM objects with mutable state and tinker their states, thus achieving object oriented programming within clojure. Otherwise, you may just use these clojure abstractions in their more naive and intended way. So without more ado let us enumerate those abstractions.

+ an api for common interface between different implementations called [_protocols_](protocols-interfaces)
+ an api for function dispatch by argument types and/or values called _multimethod_
+ an api for data types called (_datatypes_)

None of these are meant for managing mutable state within objects. They are just api for abstractions that are basic enough to be included in the core langauge. You mix and match these api as per the abstractions you wish to orient your code by, whenever you feel that they are a match for the abstraction you have in mind for your code. They are just an extra layer of abstraction which you may opt into. They also happen to facilitate Java interop, because they are implemented under-the-hood by constructs that can be used from Java code; the latter aspect we do not focus on so much, and you can easily pick it up off the official docs.
