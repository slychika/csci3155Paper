#Implementing Generics in Java#

##The Journey##

Principals of Programming Language

Heather L. Dykstra

Caitlin E. Hickey

Intro (Earth is in Danger (again)):

On May 11, 1999 the Java Specification Request of adding generic types to the Java Programming Language was approved. Years later the Final Release was published. This was on September 30, 2004 but the main community arguments happened between the two dates. From the 18th of May 1999 until August 1, 2001 the public had the opportunity to review and create the implementation. Even after such an extensive process, we could not make everyone happy. The following contains the aftermath, when the community responds to JSR 14.

Paragraph 1- Why Generics? (The Ood):
Programming with generics is a style supported by many languages (C#, C++, .Net, etc.) in which programs are written without specified types.  Instead, the programs are written with placeholders where the types would have normally been placed.  Those types are filled in later, allowing programmers to use the same method or methods to work on objects of different types.  The implementation of generics varies across languages with Java having perhaps one of the most unique implementations.  


Paragraph 2- Pros (The Companions):
The advantages of using generics include efficiency and type safety, especially with respect to collections.  Prior to generics being implemented, members of collections were treated as objects, regardless of what type of objects they were.  Code that placed objects of two or more types in a collection would compile nicely, as the compiler did not differentiate between these types, but throw errors at run time.  One of the main advantages to generic programming in Java is that once a type has been declared for a collection, the compiler will not allow you to place an object of a different type in that collection.  Generics in Java can be used in classes, collections, and methods.  


Paragraph 3- Cons (Daleks):
One of the main criticisms of generics is that they are unnecessary and unnecessarily complicated.  Ken Arnold, a blogger with Java.net, commented that the Java community had survived without generics for more than five years, and that the complexity they added outweighs the benefits of having them.  His main argument is that while generics seem simple enough, there are certain very specific instances in which they should not be used, and those instances are difficult to understand.  Additionally, a blogger on facsim.org argues that generics are basically a waste because they provide the same output as code without generics.  This blogger also commented that the Java compiler removes all traces of generics, essentially leaving the code as it would have been had you coded without them in the first place.  This is referred to as erasure, and has other side-effects that may be unwanted.  As an example, with type erasure, a List<string> would be converted to type List at compile-time.  Another problem is that generics are not co-variant.  This means that a subtype of a class cannot be substituted for an object of that class in a generics setting.  This also means that generics do not interact well with Arrays and ArrayLists because they are co-variant. 

Conclusion- Resolution (Earth is Saved (again)):
Generics is a very complicated topic, and it allows for many improvements on your code, depending on your coding style. It was an aspect that was already key to other languages and so the Java community adopted it, making it more versatile and adaptable. Even with the downfalls to the implementation, it is an exciting addition to many and it is unique to the Java community. 


Resources:

http://jcp.org/en/jsr/all

http://jcp.org/en/jsr/detail?id=14

http://openjdk.java.net/jeps/0

http://en.wikipedia.org/wiki/Generics_in_Java

http://docs.oracle.com/javase/tutorial/java/generics/types.html

http://docs.oracle.com/javase/tutorial/java/generics/why.html


-note: leaving blanks is like using generics... -
