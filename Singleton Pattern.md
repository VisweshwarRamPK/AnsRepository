**1)SINGLETON PATTERN**


### **I) DEFINITION:**

The **Singleton pattern** is a creational design pattern that ensures a class has only **one instance** and provides a global point of access to that instance. This is useful in scenarios where exactly one object is needed to coordinate actions across the system.


### **II) USE:**

The Singleton pattern is used when:



* There should be only one instance of a class that can control the entire application's resources.
* You need a **global point of access** to that instance.
* Managing **shared resources** like database connections, logging, configuration settings, etc.


### **III) CONCEPT:**



* A Singleton class restricts the instantiation of the class to one "single" instance.
* It ensures that other classes can only interact with this instance, typically using a **static method** to access the instance.
* The constructor is made **private** to prevent creating new instances outside the class.


### **IV) PROBLEM IT SOLVES:**

Without Singleton, a class can be instantiated multiple times, leading to:



* **Inconsistent behavior** across different parts of the system.
* **High memory usage** if objects are unnecessarily duplicated.


### **V) HOW TO RESOLVE:**

The Singleton pattern resolves these issues by:



* **Restricting the instantiation** of the class to a single object.
* Using a **static method** (like getInstance()) to control object creation.
* Making the constructor **private** so that only the class itself can create an instance.


### **VI) FEATURES::**



* **Lazy Instantiation**: The Singleton object is created only when it's needed, which optimizes memory use.
* **Global Access**: Singleton provides a global point of access to the instance, ensuring consistency across the application.
* **Thread Safety**: In a multi-threaded environment, Singleton may need to be implemented with locking mechanisms to avoid multiple threads creating separate instances.
* **Private Constructor**: To prevent creating objects from outside the class, its constructor is private.

**VII) IMPLEMENTATION CODE:**

public class Singleton {

    // Static variable to hold the one instance

    private static Singleton instance;

    // Private constructor to prevent instantiation

    private Singleton() { }

    // Static method to provide global access to the single instance

    public static Singleton getInstance() {

        if (instance == null) {

            instance = new Singleton();

        }

        return instance;

    }

}