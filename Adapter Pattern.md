**6) ADAPTER:**

**REAL WORLD EXAMPLE:**

Let’s say Person A speaks English, and Person B speaks Spanish. A translator acts as an intermediary, converting English into Spanish so that Person B can understand, and vice versa. The translator (adapter) doesn’t change the original language, but just makes communication possible between two people speaking different languages.


### In the context of the Adapter Pattern:



* Person A (English): The original incompatible system.
* Person B (Spanish): The system that expects a different format.
* Translator (Adapter): Converts messages from one format to another.

**I) DEFINITION:**

The Adapter pattern is used to allow two incompatible interfaces to work together. It acts as a bridge between two objects, enabling them to communicate without changing their existing code.


### **II) USE:**

The Adapter pattern is typically used in the following scenarios:



* When a class needs to use an existing class with an incompatible interface.
* When you want to create a reusable class that works with unrelated or incompatible classes.
* When you want to convert an existing interface into another interface clients expect.


### **III) CONCEPT:**

The Adapter pattern acts like a middleman. It helps two things work together, even if they weren’t originally designed to. The adapter is like a translator who converts something into a form that both sides can understand.

Here’s how it works:



* The adapter class wraps around an object that doesn't fit with what the client (or user) expects.
* The adapter listens to what the client wants, then translates the request into something that the wrapped object can understand.

Class Adapter (Using Inheritance):



* Think of this like a translator who is also a part of both cultures. They know both languages because they’ve learned them from birth, so they directly translate between them using their knowledge.
* In programming: The adapter inherits from both classes (client and service), and translates between them.

Object Adapter (Using Composition):



* Now, think of a translator who is separate from both cultures. They don’t belong to either group, but they understand both. They connect the two people by listening to one and speaking to the other.
* In programming: The adapter has a reference (or a link) to the object it’s adapting, and uses it to translate requests.

There are two types of Adapter patterns:



1. Class Adapter: Uses inheritance to adapt one interface to another.
2. Object Adapter: Uses composition to adapt one interface to another.


### **IV) PROBLEM IT SOLVES:**

The Adapter pattern solves the problem of working with incompatible interfaces without modifying the existing code. It enables objects from different libraries or frameworks to cooperate by providing an intermediary adapter.

For example, if you have a class that implements a PaymentProcessor interface and another library provides a ThirdPartyPayment class with a different interface, you can create an adapter to bridge the gap between the two.


### **V) FEATURES:**



* Reusability: The adapter allows you to reuse existing code with incompatible systems.
* Flexibility: It helps make two unrelated classes work together without modifying them.
* Loose coupling: The adapter introduces an intermediary between classes, reducing the coupling between client and service classes.


### **VI) HOW TO RESOLVE:**



1. Create an Adapter Class:
    * First, you define a new adapter class. This is like creating a translator who knows how to communicate between two different languages (or systems).
    * The adapter class will use an interface that the client (the user or system needing the service) expects.
2. Wrap the Incompatible Class:
    * Inside the adapter class, you wrap the existing incompatible class. Think of this like putting a friend who speaks English inside the translator’s (adapter's) toolkit.
    * This means the adapter holds onto the incompatible class and can use it when needed.
3. Delegate Method Calls:
    * When the client wants to call a method, the adapter takes that request and delegates (forwards) it to the wrapped class (the incompatible one). This is like the translator listening to one friend and then telling the other friend what they said.
    * The adapter translates the request into a language the wrapped class understands.
4. Convert Method Calls:
    * The adapter may need to convert or change the way the request looks so that the wrapped class can understand it. This is similar to how a translator might change phrases to fit the other language's structure.

**VII) IMPLEMENTATION CODE:**

// Target Interface

interface SpanishSpeaker {

    void speakSpanish(String message);

}

// Incompatible Class

class EnglishSpeaker {

    public void speakEnglish(String message) {

        System.out.println("English Speaker says: " + message);

    }

}

// Adapter Class

class TranslatorAdapter implements SpanishSpeaker {

    private EnglishSpeaker englishSpeaker;

    public TranslatorAdapter(EnglishSpeaker englishSpeaker) {

        this.englishSpeaker = englishSpeaker; // Wrap the incompatible class

    }

    @Override

    public void speakSpanish(String message) {

        // Translate the English message to Spanish

        // For simplicity, let's just mock the translation

        String translatedMessage = translateToSpanish(message);

        englishSpeaker.speakEnglish(translatedMessage); // Delegate the request

    }

}

// Client Code

public class Main {

    public static void main(String[] args) {

        EnglishSpeaker englishSpeaker = new EnglishSpeaker(); // Incompatible class

        SpanishSpeaker spanishSpeaker = new TranslatorAdapter(englishSpeaker); // Adapter

        // Now the Spanish speaker can communicate via the translator

        spanishSpeaker.speakSpanish("Hello, how are you?"); 

        // Output: English Speaker says: Mensaje en español: Hello, how are you?

    }

}
