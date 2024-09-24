**3) IMPLEMENT ANY LOGIC IN AN OBJECT ORIENTED WAY**

**I) INTERFACE II)ABSTRACT III)DERIVED**

**I) INTERFACE:**

An interface defines a set of abstract methods that a class must implement.

**CODE:**

interface Animal {

    void makeSound(); // No method body, just a signature

}

**II) ABSTRACT CLASS:**

An abstract class is partially implemented, meaning it can have both abstract methods (without a body) and concrete methods (with a body).

**CODE:**

abstract class Mammal implements Animal {

    void walk() {

        System.out.println("Walking...");

    }

}

**III) DERIVED CLASS:**

A derived class extends an abstract class or implements an interface, providing implementation code for abstract methods.

class Dog extends Mammal {

    @Override

    public void makeSound() {

        System.out.println("Bark");

    }

}
