#Implementing Generics in Java#

##The Journey##

Principals of Programming Language

Heather L. Dykstra

Caitlin E. Hickey

Intro (Earth is in Danger (again)):

On May 11, 1999 the Java Specification Request of adding generic types to the Java Programing Language was aproved. Years later the Final Release was published. This was on September 30, 2004 but the main community arguments happened between the two dates. From the 18th of May 1999 until August 1, 2001 the public had the opportunity to review and create the implementation. Even after such an extensive process, we could not make everyone happy. The following contains the aftermath, when the community responds to JSR 14.

Paragraph 1- Why Generics? (The Ood):


Paragraph 2- Pros (The Companions):


Paragraph 3- Cons (Daleks):


One of the main criticisms of generics is that they are unnecessary and unnecessarily complicated.  Ken Arnold, a blogger with Java.net, commented that the Java community had survived without generics for more than five years, and that the complexity they added outweighs the benefits of having them.  His main argument is that while generics seem simple enough, there are certain very specific instances in which they should not be used, and those instances are difficult to understand.    Additionally, a blogger on facsim.org argues that generics are basically a waste because they provide the same output as code without generics.  This blogger also commented that the Java compiler removes all traces of generics, essentially leaving the code as it would have been had you coded without them in the first place.  This is referred to as erasure, and has other side-effects that may be unwanted.  As an example, with type erasure, a List<string> would be converted to type List at compile-time.  Another problem is that generics are not covariant.  This means that a subtype of a class cannot be substituted for an object of that class in a generics setting.  This also means that generics do not interact well with Arrays and ArrayLists because they are covariant. 

Conclusion- Resolution (Earth is Saved (again)):


Resources:

http://jcp.org/en/jsr/all

http://jcp.org/en/jsr/detail?id=14

http://openjdk.java.net/jeps/0

http://en.wikipedia.org/wiki/Generics_in_Java

http://docs.oracle.com/javase/tutorial/java/generics/types.html

http://docs.oracle.com/javase/tutorial/java/generics/why.html
