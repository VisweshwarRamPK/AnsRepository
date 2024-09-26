**7) VISITOR:**

**REAL WORLD EXAMPLE:**

Imagine you're in a large museum filled with different types of exhibits—paintings, sculptures, and ancient artifacts. Each type of exhibit tells a different story and needs a different kind of explanation.

Now, imagine that the museum hires specialized tour guides. One guide is an expert in paintings, another in sculptures, and a third in ancient artifacts. When you visit the museum, depending on the type of exhibit you're looking at, a different guide steps in to explain it to you.

In this analogy:



* The exhibits (paintings, sculptures, artifacts) are like the elements in the Visitor design pattern. They stay the same and don't change.
* The tour guides are like the visitors in the pattern. Each guide knows how to explain one type of exhibit very well.

The cool part is, the museum doesn't need to change its exhibits whenever a new guide (with new knowledge) is hired. Similarly, in the Visitor design pattern, new operations (like new guides) can be added without changing the objects they work on (the exhibits).

**I) DEFINITION:**

The Visitor Pattern is a design pattern that allows adding further operations or behaviors to a set of classes without altering their code.This pattern allows one to add new functionality to an object structure by defining a new visitor class.

**II) USE:**

When the object structure rarely changes but new operations are frequently added.

When you want to add operations together, and define operations for a class without changing the class.


### **IV) PROBLEM IT SOLVES:**



* Difficulty in Adding New Operations: In a traditional object-oriented system, adding new operations requires modifying each class. This violates the Open-Closed Principle (OCP), which states that software entities should be open for extension but closed for modification.
* Tight Coupling of Classes and Operations: In systems where multiple operations are required on object structures, coupling operations with classes makes the system rigid and hard to maintain or extend.


### **V) HOW TO RESOLVE:**

The Visitor Pattern resolves these issues by:



* Decoupling operations from the object structure(class). Instead of embedding operations in the classes, it moves them to a separate visitor class.
* Allowing new operations to be added without modifying the existing structure. The object structure remains stable, while the operations (visitors) are free to change.

**VI) FEATURES:**

Extensibility: Adding new operations becomes easier without modifying existing classes.

Separation of Concerns: It separates the algorithm and object structure, enhancing maintainability.

**VII) IMPLEMENTATION CODE:**

interface Exhibit {

    void accept(TourGuide guide);

}

class Painting implements Exhibit {

    void accept(TourGuide guide) { guide.visit(this); }

    String getDetails() { return "Renaissance painting."; }

}

class Sculpture implements Exhibit {

    void accept(TourGuide guide) { guide.visit(this); }

    String getDetails() { return "Greek sculpture."; }

}

class Artifact implements Exhibit {

    void accept(TourGuide guide) { guide.visit(this); }

    String getDetails() { return "Roman artifact."; }

}

interface TourGuide {

    void visit(Painting painting);

    void visit(Sculpture sculpture);

    void visit(Artifact artifact);

}

class Guide implements TourGuide {

    public void visit(Painting p) { System.out.println(p.getDetails()); }

    public void visit(Sculpture s) { System.out.println(s.getDetails()); }

    public void visit(Artifact a) { System.out.println(a.getDetails()); }

}

public class MuseumTour {

    public static void main(String[] args) {

        Exhibit[] exhibits = { new Painting(), new Sculpture(), new Artifact() };

        TourGuide guide = new Guide();

        for (Exhibit exhibit : exhibits) {

            exhibit.accept(guide);

        }

    }

}
