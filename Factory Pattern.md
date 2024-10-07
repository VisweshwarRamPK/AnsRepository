**2)FACTORY PATTERN:**

**I)DEFINITION:**

The **Factory Pattern** defines an interface or abstract class for creating an object, but allows the subclasses to decide which class to instantiate. It helps in decoupling the object creation process from the client code, making the code more modular and easier to maintain.


### **II) USE:**



* When the creation process of objects is complex.
* When you have a set of related or dependent objects that follow a common interface, but the specific object to be called depends on the runtime conditions.


### **III) CONCEPT:**



* The Factory pattern provides an interface or abstract class to define the object creation method.
* Subclasses implement this creation method and decide which concrete class to instantiate.
* The client uses the factory method instead of directly instantiating objects.

In Java, the factory pattern typically involves the following components:



1. **Product (Interface)**: An interface that defines the object to be created.
2. **Concrete Product**: The actual class that implements the Product interface.
3. **Factory**: A class responsible for creating objects that implement the Product interface.
4. **Concrete Factory**: A subclass of the Factory class that decides which concrete product to instantiate.


### **IV) PROBLEM IT SOLVES:**

Without the factory pattern, the client code would be tightly coupled with the concrete classes it instantiates. This makes the code difficult to extend and maintain. If new object types are added, the client code needs to be updated, violating the **Open/Closed Principle**.


### **V) HOW TO RESOLVE:**

The factory pattern resolves this issue by delegating the responsibility of object creation to a factory class. The client interacts with the factory rather than directly with the concrete classes. This promotes loose coupling and flexibility, as the client is unaware of the specific class being instantiated.


### **VI) FEATURES:**



1. **Encapsulation of Object Creation**: Hides the creation logic from the client.
2. **Loose Coupling**: The client code is decoupled from the concrete classes.
3. **Code Reusability**: Reduces code duplication by centralizing the object creation logic.

**VII) IMPLEMENTATION CODE:**

// Step 1: Create the Product interface

interface Animal {

    void speak();

}

// Step 2: Implement Concrete Products

class Dog implements Animal {

    @Override

    public void speak() {

        System.out.println("Woof! Woof!");

    }

}

class Cat implements Animal {

    @Override

    public void speak() {

        System.out.println("Meow! Meow!");

    }

}

// Step 3: Create the Factory class

class AnimalFactory {

    // Factory method

    public static Animal createAnimal(String type) {

        if ("Dog".equalsIgnoreCase(type)) {

            return new Dog();

        } else if ("Cat".equalsIgnoreCase(type)) {

            return new Cat();

        }

        throw new IllegalArgumentException("Unknown animal type");

    }

}

// Step 4: Client code

public class FactoryPatternDemo {

    public static void main(String[] args) {

        // Create a Dog object using the factory

        Animal dog = AnimalFactory.createAnimal("Dog");

        dog.speak();  // Output: Woof! Woof!

        // Create a Cat object using the factory

        Animal cat = AnimalFactory.createAnimal("Cat");

        cat.speak();  // Output: Meow! Meow!

    }

}

Example of Factory Pattern:
```java
EmployeeFactory.java
package com.example.jdbc.factory;

import com.example.jdbc.repository.EmployeeRepository;
import com.example.jdbc.service.EmployeeService;
import com.example.jdbc.util.JsonToXmlConverter;

public interface EmployeeFactory {
    EmployeeService createEmployeeService();
    EmployeeRepository createEmployeeRepository();
    JsonToXmlConverter createJsonToXmlConverter();
}
DefaultEmployeeFactory.java
package com.example.jdbc.factory;

import com.example.jdbc.repository.EmployeeRepository;
import com.example.jdbc.service.EmployeeService;
import com.example.jdbc.util.JsonToXmlConverter;
import org.springframework.stereotype.Component;

@Component
public class DefaultEmployeeFactory implements EmployeeFactory {

    @Override
    public EmployeeService createEmployeeService() {
        return new EmployeeService(createEmployeeRepository());
    }

    @Override
    public EmployeeRepository createEmployeeRepository() {
        return new EmployeeRepository();
    }

    @Override
    public JsonToXmlConverter createJsonToXmlConverter() {
        return new JsonToXmlConverter();
    }
}
EmployeeController:
package com.example.jdbc.controller;

import com.example.jdbc.factory.EmployeeFactory;
import com.example.jdbc.service.EmployeeService;
import com.example.jdbc.util.JsonToXmlConverter;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.RequestMapping;

@RestController
@RequestMapping("/employees")
public class EmployeeController {

    private final EmployeeService employeeService;
    private final JsonToXmlConverter jsonToXmlConverter;

    public EmployeeController(EmployeeFactory employeeFactory) {
        this.employeeService = employeeFactory.createEmployeeService();
        this.jsonToXmlConverter = employeeFactory.createJsonToXmlConverter();
    }
}

