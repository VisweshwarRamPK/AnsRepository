**11) LAMBDA EXPRESSIONS:**

** LAMBDA EXPRESSIONS:**

**I) DEFINITION:**

**A lambda expression is a short block of code which takes in parameters and returns a value.It is also called an anonymous function,that is a function without a name.**

**It is used in Functional Interfaces and streams.**

**Introduced in: Java 8.**

**Syntax:**

**(parameters) -> expression**

**II) USE:**

**Code Simplification: They reduce the boilerplate code, especially when using functional interfaces like <code>Runnable</code>, <code>Comparator</code>, or <code>Callable</code>.</strong>

**Works mainly with interfaces that have only one method (called functional interfaces).**

**III) LAMBDA WITH FUNCTIONAL INTERFACE:**

** A functional interface is an interface that has only one abstract method. Lambda expressions work with these interfaces.**

**Example of a functional interface:**

**CODE:**

**@FunctionalInterface**

**interface MyFunctionalInterface {**

**    void doSomething();**

**}**

**MyFunctionalInterface func = () -> System.out.println("Doing something");**

**func.doSomething();  // Output: Doing something**

**IV) LAMBDA WITH STREAMS:**

** Lambda expressions work very well with the Streams API introduced in Java 8.**

**CODE:**

**List&lt;Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);**

**numbers.stream().filter(n -> n % 2 == 0).collect(Collectors.toList());**

**V) POINTS:**

**Single-method Interfaces: Lambda expressions are designed to work with functional interfaces (interfaces with a single abstract method).**

**Reduces boilerplate code, making code more concise and readable.**

**VI) FINAL EXAMPLE WITH RUNNABLE:**

**Example Without Lambda:**

**Runnable r = new Runnable() {**

**    public void run() {**

**        System.out.println("Hello!");**

**    }**

**};**

**Example With Lambda:**

**Runnable r = () -> System.out.println("Hello!");**

Implementation of Lambda Expressions:
In findById Method:
```java
return employeeRepository.findById(id)
    .orElseThrow(() -> {
        logger.error("Employee with id: {} not found", id);
        return new EmployeeNotFoundException(id);
    });
```
In update Method:
```java
return employeeRepository.findById(id)
    .map(existingEmployee -> {
        employee.setId(id); // Set the employee ID for update
        logger.info("Employee updated with id: {}", id);
        return employeeRepository.save(employee);
    })
    .orElseThrow(() -> {
        logger.error("Employee with id: {} not found for update", id);
        return new EmployeeNotFoundException(id);
    });
```
