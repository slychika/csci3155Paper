#Implementing Generics in Java#

Principals of Programming Language

Heather L. Dykstra

Caitlin E. Hickey

Michael D. Williams

Programming with generics is a style supported by many languages (C#, C++, .Net, etc.) in which programs are written without specified types.  Instead, the programs are written with placeholders where the types would have normally been placed.  Those types are filled in later, allowing programmers to use the same method or methods to work on objects of different types. This style of programming was put up as a Java Specification Request and was soon implemented. While most people were in support of adding generics to Java, many people were unhappy with the method of implementation that Oracle used. The general implementation of generics varies across languages but Java has perhaps one of the most unique and frustrating implementations.

On May 11, 1999 the Java Specification Request of adding generic types to the Java Programming Language was approved.  The final release was published on September 30, 2004 but the main community arguments happened between the two dates. From the 18th of May 1999 until August 1, 2001 the public had the opportunity to review and create the implementation. 

In support of Java Generics, Gilad Bracha who helped implement JSR 14 said, "Calling legacy code from generic code is inherently dangerous; once you mix generic code with non-generic legacy code, all the safety guarantees that the generic type system usually provides are void. However, you are still better off than you were without using generics at all. At least you know the code on your end is consistent." This exemplifies the advantages of using generics, especially in specific cases. Other advantages to Java Generics include efficiency and type safety, especially with respect to collections.  Prior to generics being implemented, members of collections were treated as objects, regardless of what type of object they were. Code that placed objects of two or more types in a collection would compile nicely, as the compiler did not differentiate between these types, but threw errors at run time. Below is an example of code that will compile but throw runtime errors: 
    
    List v = new ArrayList();
      v.add("test");
      Integer i = (Integer)v.get(0);

The problem is that the code adds a string to a List, but then tries to retrieve that string as an integer.  Adding generics to Java solved problems like the one above.  One of the other main advantages to generic programming in Java is that once a type has been declared for a collection, the compiler will not allow you to place an object of a different type in that collection.  Generics in Java can be used in classes, collections, and methods.  Another advantage to generics is that programmers do not necessarily have to know what type of object will be used by a method they are writing, just that the type supports the operator or operators which they are using in the method.  A classic example is the max method below:

    template <typename T>
    T max (T a, T b){
    return (b < a) ? a : b;
    } 

Any type can work with this method, so long as the less than (<) operator is defined for that type. 

Java generics also implemented something known as wildcard types. Wildcard types, written List<?>, are the supertype of lists. The compiler would read this as a List of unknown because you can't add anything, except null, to List<?>, but you can retrieve things and treat them as Objects. Wildcards can have upper and lower bounds, where List<? extends Drinks> would be a List of items that have unknown type but are Drinks and List<? super Drinks> is a List of items that have an unknown type but are supertypes of Drinks. You would use an upper bound wildcard for reading/input and a lower bound wildcard for writing/output. Here's some example code using wildcards:

    class Bar<T> {
        void buy(int howMany, List<? super T> fillDrink {... }
        void puke(List<? extends T> throwUpDrink) {...}
        ...
    }

    Bar<Drink> bartender = new Bar<Drink>();
    List<Vodka> shot = ...;
    List<Shot> tooMuchAlcohol = ...;
    
    //Buy vodka from the Bar
    bartender.buy(3, shot);
    //You can puke up the shot the Bar gave you...
    bartender.puke(tooMuchAlcohol);

So you can buy from the bartender, (with super), and you can puke up your drink (with extend). 

While this implementation of generics made many community members happy, there were a lot of unhappy members as well. One of the main criticisms of generics is that they are unnecessary and unnecessarily complicated.  Ken Arnold, a blogger with Java.net, commented that the Java community had survived without generics for more than five years, and that the complexity they added outweighs the benefits of having them.  His main argument is that while generics seem simple enough, there are certain very specific instances in which they should not be used, and those instances are difficult to understand.  Additionally, a blogger on facsim.org argues that generics are basically a waste because they provide the same output as code without generics.  This blogger also commented that the Java compiler removes all traces of generics, essentially leaving the code as it would have been had you coded without them in the first place.  
This is referred to as erasure, and has other side-effects that may be unwanted.  The purpose of this implementation was to allow the Java community to use generics without having to make significant changes to the Java Virtual Machine. While erasure allows for backwards compatibility allowing for legacy non-generic libraries, you can't see what type a generic class is using at run-time. As an example, with type erasure, a List<string> would be converted to type List at compile-time.  Another problem is that generics are not co-variant.  This means that a subtype of a class cannot be substituted for an object of that class in a generics setting:
 

    List<Towel> towels = new ArrayList<Towel>();
    List<Object> objs = towels;
    objs.add(new JellyBeans());
    Towel a = towels.remove(0);

The last line of this code would assign JellyBeans to Towel, which obviously is a problem. This also means that generics do not interact well with Arrays and ArrayLists because they are co-variant and generics are not. 
The next piece of code is an example that we still cannot fix with our implementation of generics 

    Item[] chalk = new Item[3];
    Object[] objs = chalk;
    objs[0] = new crayon();

The Java compiler allows the second line to run and the third line becomes an ArrayStoreException, meaning that the program tried to store the wrong type of object into an array of objects.  If this were allowed or properly written with generics, it would break the type safety that generics are supposed to provide.  It should be noted here that the JVM only tests for type safety at compile time.  After that, there is no more checking for safety.

Another disadvantage of the way generics are implemented in Java is that all instantiations of a generic type declaration must share the same runtime implementation.  This can lead to a phenomenon known as heap pollution- where a variable of a certain type points to a variable of the different type. The following is an example: 

    List ln = new ArrayList<Number>(); 
     List<String> ls =ln;  // unchecked warning 
     String s = ls.get(0);  // ClassCastException

The problem with this is that ls ends up pointing to an object of a completely different type.  This is partially made possible by erasure, and will likely result in a ClassCastException at runtime, but will not cause a compile time error.

Generics are complicated and due to the way that Oracle implemented them, people argue frequently about their usefulness. Had Oracle approached the problem differently and been willing to change the Java Virtual Machine (or JVM), they could have made a better addition to the Java library which the general community might use much more often. However, generics are useful in certain specific circumstances and many coders use them despite their drawbacks.  



Resources:

http://jcp.org/en/jsr/all

http://jcp.org/en/jsr/detail?id=14

http://openjdk.java.net/jeps/0

http://en.wikipedia.org/wiki/Generics_in_Java

http://docs.oracle.com/javase/tutorial/java/generics/types.html

http://docs.oracle.com/javase/tutorial/java/generics/why.html

http://www.cs.umd.edu/users/meesh/420/Notes/JAVANotes/java_generics-jmeister.pdf

http://www.angelikalanger.com/GenericsFAQ/FAQSections/TechnicalDetails.html#What is heap pollution?

http://lambda-the-ultimate.org/node/804

http://www.ibm.com/developerworks/java/library/j-jtp01255/index.html

http://programmers.stackexchange.com/questions/22642/what-is-wrong-with-javas-generics

http://stereolambda.com/2009/10/23/java-generics-were-they-a-good-idea/

http://c2.com/cgi/wiki?GenericProgrammingIsBetter