**5)STATE PATTERN:**

**REAL WORLD EXAMPLE:**

In a traffic light system, the Context is the traffic light itself, which can be in one of three states: Green, Yellow, or Red. Each of these states controls how the traffic light behaves—whether cars should go, slow down, or stop. The State Interface defines what each state should do, and each specific state (Green, Yellow, or Red) has its own class that manages its behavior. Instead of using a lot of `if-else` statements to check which light is on, we separate the behavior for each state into its own class. This way, when the traffic light changes from Green to Yellow, it simply switches to the appropriate state class, and the behavior changes automatically without needing complicated checks.


### **I) DEFINITION:**

The State Pattern is a behavioral design pattern that allows an object to change its behavior when its internal state changes. This pattern is useful when an object has multiple states, and its behavior varies based on its current state


### **II) USE:**

The State Pattern is primarily used when:



* An object's behavior depends on its state.
* The object can transition between different states at runtime.
* You want to avoid large conditional (if-else or switch) statements for handling state-specific behavior.

**III) CONCEPT:**

Context: This is the class whose behavior varies depending on its internal state.

State Interface: This defines the common interface for all possible states,Each concrete state implements this interface.

Concrete States: These are the specific implementations of the state interface.


### **IV. PROBLEM IT SOLVES:**

In scenarios where an object’s behavior changes with its state, developers tend to use conditional logic (if-else or switch statements) to manage different behaviors. This leads to tightly coupled, difficult-to-maintain code.


### **V. HOW IT RESOLVES:**

The State Pattern resolves this problem by:



* Encapsulating state-specific behavior into separate classes.
* Allowing the context object to change its state without directly modifying the code in the context.
* Promoting better organization and maintenance by avoiding long conditional statements.


### **VI. FEATURES:**



* Encapsulation of state-specific behavior: Each state is represented as a separate class that handles its own behavior.
* Separation of concerns: The context class is only responsible for managing state transitions, while each state class manages its behavior.
* Open/Closed Principle: Adding new states doesn’t require modifying the context or other state classes.

**VII) IMPLEMENTATION CODE IN JAVA:**

// State Interface

interface TrafficLightState {

    void handle();

}

// Green State: Cars are allowed to pass.

class GreenState implements TrafficLightState {

    @Override

    public void handle() {

        System.out.println("Green Light: Cars can go.");

    }

}

// Yellow State: Cars should prepare to stop.

class YellowState implements TrafficLightState {

    @Override

    public void handle() {

        System.out.println("Yellow Light: Cars should slow down and prepare to stop.");

    }

}

// Red State: Cars must stop.

class RedState implements TrafficLightState {

    @Override

    public void handle() {

        System.out.println("Red Light: Cars must stop.");

    }

}

// Context: Traffic Light that changes states

class TrafficLight {

    private TrafficLightState currentState;

    public void setState(TrafficLightState state) {

        this.currentState = state;

    }

    public void changeLight() {

        currentState.handle();

    }

}

// Main class to demonstrate the Traffic Light System

public class TrafficLightSystem {

    public static void main(String[] args) {

        TrafficLight trafficLight = new TrafficLight();

        TrafficLightState green = new GreenState();

        TrafficLightState yellow = new YellowState();

        TrafficLightState red = new RedState();

        // Traffic Light is Green

        trafficLight.setState(green);

        trafficLight.changeLight();

        // Traffic Light turns Yellow

        trafficLight.setState(yellow);

        trafficLight.changeLight();

        // Traffic Light turns Red

        trafficLight.setState(red);

        trafficLight.changeLight();

    }

}