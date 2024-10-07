**3)OBSERVER:**


### **I) DEFINITION:**

The **Observer Pattern** is like a subscription system. One object (called the subject) can be watched by many other objects (called observers). Whenever something changes in the subject, it tells all its observers about the change. This is useful in situations where multiple parts of a system need to react to an event, like when a button is clicked in a graphical user interface (GUI) or when real-time data is updated.

So, instead of each observer constantly checking for changes, the subject automatically notifies them when something happens.


### **II) USE**

The Observer pattern is used when:



* An object needs to notify other objects of changes without being tightly coupled to those objects.
* Multiple objects need to be updated automatically when an event occurs in the subject.
* You want to decouple the subject from the concrete observers, allowing for dynamic addition/removal of observers.


### **III) CONCEPT**

The Observer pattern involves two main types of components:



* **Subject (Observable)**: The object whose state changes. It maintains a list of dependents (observers) and notifies them when its state changes.
* **Observer**: The objects that depend on the subject's state. They subscribe to the subject and are updated whenever there is a change in the subject.


### **IV) PROBLEM IT SOLVES:**

The **Observer Pattern** solves the problem of keeping several objects (observers) updated when something changes in another object (the subject) without making them too dependent on each other.

Without this pattern, you would need to write complicated code to make sure every object knows about the changes, which can easily lead to mistakes and messy code. The Observer Pattern makes it easy for the subject to notify all its observers automatically whenever something changes, saving you from writing error-prone, repetitive code.


### **V) HOW TO RESOLVE:**

The problem of updating multiple observers is resolved by creating a **Subject** class that maintains a list of observers. When the state of the subject changes, the subject iterates through the list and notifies all observers. This decouples the subject from the observers, allowing the observers to be dynamically added or removed without changing the subject's logic.


### **VI) FEATURES:**



* **Decoupling**: Observers and the subject are loosely coupled. The subject doesn't need to know anything about the observers.
* **Dynamic**: Observers can be added or removed at runtime, making it flexible for various use cases.
* **One-to-many relationship**: One subject can have multiple observers, and all are notified of changes in the subject.

**VII) REAL WORLD EXAMPLE:**

In simple terms, imagine a news agency that writes articles. There are several news outlets, like TV stations or websites, that want to know when the agency publishes something new. These outlets "subscribe" to the news agency. Every time the agency publishes a new article, it automatically tells all the subscribed outlets. The outlets can then show the latest news to their viewers, whether it's on TV, online, or in print.

The key idea is that the news agency doesn't need to know how each outlet shows the news. It just sends out the update, and each outlet handles it in its own way. This makes the system flexible because the news agency and the outlets are loosely connected.

**VIII) IMPLEMENTATION CODE IN JAVA:**

// Step 1: Define the Observer interface

interface Observer {

    void update(String message);

}

// Step 2: Define the Subject (Observable) class

import java.util.ArrayList;

import java.util.List;

class Subject {

    private List&lt;Observer> observers = new ArrayList&lt;>();

    private String message;

    // Register an observer

    public void addObserver(Observer observer) {

        observers.add(observer);

    }

    // Unregister an observer

    public void removeObserver(Observer observer) {

        observers.remove(observer);

    }

    // Notify all observers of the change

    public void notifyObservers() {

        for (Observer observer : observers) {

            observer.update(message);

        }

    }

    // Change state and notify observers

    public void setMessage(String message) {

        this.message = message;

        notifyObservers();

    }

}

// Step 3: Define concrete observers

class ConcreteObserver1 implements Observer {

    @Override

    public void update(String message) {

        System.out.println("ConcreteObserver1 received: " + message);

    }

}

class ConcreteObserver2 implements Observer {

    @Override

    public void update(String message) {

        System.out.println("ConcreteObserver2 received: " + message);

    }

}

// Step 4: Testing the Observer Pattern

public class ObserverPatternDemo {

    public static void main(String[] args) {

        Subject subject = new Subject();

        Observer observer1 = new ConcreteObserver1();

        Observer observer2 = new ConcreteObserver2();

        subject.addObserver(observer1);

        subject.addObserver(observer2);

        subject.setMessage("First Update"); // Both observers receive this message

        subject.setMessage("Second Update"); // Both observers receive this message again

        subject.removeObserver(observer1);

        subject.setMessage("Third Update"); // Only observer2 receives this message

    }

}

Example of observer pattern:
Observer Interface
```java
package com.example.jdbc.observer;

public interface EmployeeObserver {
    void onEmployeeCreated(long id);
    void onEmployeeUpdated(long id);
    void onEmployeeDeleted(long id);
}
```
Concrete Observer
```java
package com.example.jdbc.observer;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class EmployeeLogger implements EmployeeObserver {
    private static final Logger logger = LoggerFactory.getLogger(EmployeeLogger.class);

    @Override
    public void onEmployeeCreated(long id) {
        logger.info("Employee with ID {} created.", id);
    }

    @Override
    public void onEmployeeUpdated(long id) {
        logger.info("Employee with ID {} updated.", id);
    }

    @Override
    public void onEmployeeDeleted(long id) {
        logger.info("Employee with ID {} deleted.", id);
    }
}
```
Service Class with Observer Management
```java
package com.example.jdbc.service;

import com.example.jdbc.model.Employee;
import com.example.jdbc.observer.EmployeeObserver;
import com.example.jdbc.repository.EmployeeRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import java.util.ArrayList;
import java.util.List;

@Service
public class EmployeeService {
    @Autowired
    private EmployeeRepository employeeRepository;

    private final List<EmployeeObserver> observers = new ArrayList<>();

    public void registerObserver(EmployeeObserver observer) {
        observers.add(observer);
    }

    public void unregisterObserver(EmployeeObserver observer) {
        observers.remove(observer);
    }

    private void notifyObservers(String action, long id) {
        for (EmployeeObserver observer : observers) {
            switch (action) {
                case "create":
                    observer.onEmployeeCreated(id);
                    break;
                case "update":
                    observer.onEmployeeUpdated(id);
                    break;
                case "delete":
                    observer.onEmployeeDeleted(id);
                    break;
            }
        }
    }

    public String createEmployee(Employee employee) {
        String result = employeeRepository.createEmployee(employee);
        if (result.equals("Employee created successfully")) {
            notifyObservers("create", employee.getId());
        }
        return result;
    }

    public String updateEmployee(Long id, Employee employee) {
        String result = employeeRepository.updateEmployee(id, employee);
        if (result.equals("Employee updated successfully")) {
            notifyObservers("update", id);
        }
        return result;
    }

    public String deleteEmployee(Long id) {
        String result = employeeRepository.deleteEmployee(id);
        if (result.equals("Employee deleted successfully")) {
            notifyObservers("delete", id);
        }
        return result;
    }
}
```
