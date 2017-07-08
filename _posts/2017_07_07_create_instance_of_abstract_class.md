https://stackoverflow.com/a/13671003

Here, i'm creating instance of my class
No, you are not creating the instance of your abstract class here. Rather you are creating an instance of an anonymous subclass of your abstract class. And then you are invoking the method on your abstract class reference pointing to subclass object.

This behaviour is clearly listed in JLS - Section # 15.9.1: -

If the class instance creation expression ends in a class body, then the class being instantiated is an anonymous class. Then:

If T denotes a class, then an anonymous direct subclass of the class named by T is declared. It is a compile-time error if the class denoted by T is a final class.
If T denotes an interface, then an anonymous direct subclass of Object that implements the interface named by T is declared.
In either case, the body of the subclass is the ClassBody given in the class instance creation expression.
The class being instantiated is the anonymous subclass.
Emphasis mine.

Also, in JLS - Section # 12.5, you can read about the Object Creation Process. I'll quote one statement from that here: -

Whenever a new class instance is created, memory space is allocated for it with room for all the instance variables declared in the class type and all the instance variables declared in each superclass of the class type, including all the instance variables that may be hidden.

Just before a reference to the newly created object is returned as the result, the indicated constructor is processed to initialize the new object using the following procedure:
You can read about the complete procedure on the link I provided.

To practically see that the class being instantiated is an Anonymous SubClass, you just need to compile both your classes. Suppose you put those classes in two different files:

My.java:

abstract class My {
    public void myMethod() {
        System.out.print("Abstract");
    }
}
Poly.java:

class Poly extends My {
    public static void main(String a[]) {
        My m = new My() {};
        m.myMethod();
    }
}
Now, compile both your source files:

javac My.java Poly.java
Now in the directory where you compiled the source code, you will see the following class files:

My.class
Poly$1.class  // Class file corresponding to anonymous subclass
Poly.class
See that class - Poly$1.class. It's the class file created by the compiler corresponding to the anonymous subclass you instantiated using the below code:

new My() {};
So, it's clear that there is a different class being instantiated. It's just that, that class is given a name only after compilation by the compiler.

In general, all the anonymous subclasses in your class will be named in this fashion:

Poly$1.class, Poly$2.class, Poly$3.class, ... so on
Those numbers denote the order in which those anonymous classes appear in the enclosing class.
