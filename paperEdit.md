#Implementing Generics in Java#

Principals of Programming Language

Heather L. Dykstra

Caitlin E. Hickey

Michael D. Williams

-We are at 832 words without code, comments, titles and reasources...

Programming with generics is a style supported by many languages (C#, C++, .Net, etc.) in which programs are written without specified types.  Instead, the programs are written with placeholders where the types would have normally been placed.  Those types are filled in later, allowing programmers to use the same method or methods to work on objects of different types. This style of programming was put up as a Java Specification Request and was soon implemented. While most people were in support of adding generics to Java, many people were unhappy with the method of implementation that Oracle used. The general implementation of generics varies across languages but Java has perhaps one of the most unique and frustrating implementations.

On May 11, 1999 the Java Specification Request of adding generic types to the Java Programming Language was approved.  The final release was published on September 30, 2004 but the main community arguments happened between the two dates. From the 18th of May 1999 until August 1, 2001 the public had the opportunity to review and create the implementation. 

In support of Java Generics, Gilad Bracha said, "Calling legacy code from generic code is inherently dangerous; once you mix generic code with non-generic legacy code, all the safety guarantees that the generic type system usually provides are void. However, you are still better off than you were without using generics at all. At least you know the code on your end is consistent." This explifies the advantages of using generics, especially in specific cases. Other advantages to Java Generics include efficiency and type safety, especially with respect to collections.  Prior to generics being implemented, members of collections were treated as objects, regardless of what type of object they were. Code that placed objects of two or more types in a collection would compile nicely, as the compiler did not differentiate between these types, but threw errors at run time. Below is an example of code that will compile but throw runtime errors: 
	
	List v = new ArrayList();
  	v.add("test");
  	Integer i = (Integer)v.get(0);

The problem is that the code adds a string to a List, but then tries to retrieve that string as an integer.  Adding generics to Java solved problems like the one above.  One of the other main advantages to generic programming in Java is that once a type has been declared for a collection, the compiler will not allow you to place an object of a different type in that collection.  Generics in Java can be used in classes, collections, and methods.  Another advantage to generics is that programmers do not necessarily have to know what type of object will be used by a method they are writing, just that the type supports the operator or operators which they are using in the method.  A classic example is the max method below:

	template <typename T>
	T max (T a, T b){
	return (b < a) ? a : b;
	} 

Any type can work with this method, so long as the less than (<) operator is defined for that type.  

	*** seems really short compared to cons... also, do we want to use more code examples here?  I thought I had a few in an earlier version...
	***maybe add something about migration compatibility? river's journal pg 55

One of the main criticisms of generics is that they are unnecessary and unnecessarily complicated.  Ken Arnold, a blogger with Java.net, commented that the Java community had survived without generics for more than five years, and that the complexity they added outweighs the benefits of having them.  His main argument is that while generics seem simple enough, there are certain very specific instances in which they should not be used, and those instances are difficult to understand.  Additionally, a blogger on facsim.org argues that generics are basically a waste because they provide the same output as code without generics.  This blogger also commented that the Java compiler removes all traces of generics, essentially leaving the code as it would have been had you coded without them in the first place.  This is referred to as erasure, and has other side-effects that may be unwanted.  The purpose of this implementation was to allow the Java community to use generics without having to make signigicant changes to the Java Virtual Machine. While erasure allows for backwards compatibility allowing for legacy non-generic libraries, you can't see what type a generic class is using at run-time. As an example, with type erasure, a List<string> would be converted to type List at compile-time.  Another problem is that generics are not co-variant.  This means that a subtype of a class cannot be substituted for an object of that class in a generics setting:

	***do we want to talk more about complexity? 

	List<Towel> towels = new ArrayList<Towel>();
	List<Object> objs = towels;
	objs.add(new JellyBeans());
	Towel a = towels.remove(0);

The last line of this code would assign JellyBeans to Towel, which obviously is a problem. This also means that generics do not interact well with Arrays and ArrayLists because they are co-variant. As an example, look at this code: 

	Item[] chalk = new Item[3];
	Object[] objs = chalk;
	objs[0] = new crayon();

The Java compiler allows the second line to run and the third line becomes an ArrayStoreException, meaning that the program tried to store the wrong type of object into an array of objects.  It should be noted here that the JVM only tests for type safety at compile time.  After that, there is no more checking for safety, which contributes to the problems demonstrated above.

Another disadvantage of the way generics are implemented in Java is that all instantiations of a generic type declaration must share the same runtime implementation.  This can lead to a phenomenon known as heap pollution- where a variable of a certain type points to a variable of the different type. The following is an example: 

	List ln = new ArrayList<Number>(); 
 	List<String> ls =ln;  // unchecked warning 
 	String s = ls.get(0);  // ClassCastException

The problem with this is that ls ends up pointing to an object of a completely different type.  This is partially made possible by erasure, and will likely result in a ClassCastException at runtime, but will not cause a compile time error.

	***need to make some kind of closing remark here about the cons- need to end this section nicely somehow.  Also, do we want multiple paragraphs for cons?  - Yes-h




Resources:

http://jcp.org/en/jsr/all

http://jcp.org/en/jsr/detail?id=14

http://openjdk.java.net/jeps/0

http://en.wikipedia.org/wiki/Generics_in_Java

http://docs.oracle.com/javase/tutorial/java/generics/types.html

http://docs.oracle.com/javase/tutorial/java/generics/why.html

http://www.cs.umd.edu/users/meesh/420/Notes/JAVANotes/java_generics-jmeister.pdf

http://www.angelikalanger.com/GenericsFAQ/FAQSections/TechnicalDetails.html#What is heap pollution?
