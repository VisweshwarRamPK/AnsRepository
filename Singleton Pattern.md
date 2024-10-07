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


Example of Singleton Design Pattern:
```java
package com.example.jdbc.util;

import java.io.IOException;

public class JsonToXmlConverter {
    private static JsonToXmlConverter instance;

    private JsonToXmlConverter() {
    }

    public static JsonToXmlConverter getInstance() {
        if (instance == null) {
            instance = new JsonToXmlConverter();
        }
        return instance;
    }

    public String convertJsonToXml(String json) throws IOException {
        if (json == null || json.isEmpty()) {
            throw new IOException("Input JSON is empty or null");
        }
        return "<root>" + json + "</root>";
    }

    public String convertXmlToJson(String xml) throws IOException {
        if (xml == null || xml.isEmpty()) {
            throw new IOException("Input XML is empty or null");
        }
        return xml.replace("<root>", "").replace("</root>", ""); // Example: remove root element
    }
}
```
