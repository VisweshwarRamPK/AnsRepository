**4)FACADE PATTERN**

**REAL WORLD EXAMPLE:**

Think of a home theater system with different devices like a DVD player, projector, speakers, and lights. Each of these devices has lots of settings and buttons, which can make using them complicated. To make things easier, you have a remote control (called the Facade) that simplifies everything. Instead of dealing with each device separately, the remote has simple buttons like "Play Movie," "Pause," or "Volume Up." When you press these buttons, the remote handles all the complicated stuff in the background, communicating with the devices to do exactly what you want. This way, you can enjoy the system without worrying about the details of each part.

**I) DEFINITION:**

The **Facade Pattern** is a design pattern that simplifies how you interact with a complex system. Instead of dealing with many complicated parts, it provides an easy-to-use interface that hides all the details. In Java, this pattern is commonly used to make it easier for a client to work with complicated libraries or systems by wrapping them in a simpler interface.

**II) USE:**



* Make a complex system easier to use by providing a simple interface.
* Make the code easier to read and understand.
* Reduce the connections between the client and the complex system, making them less dependent on each other.
* Hide unnecessary details from the client.
* Use it when you want to simplify how multiple classes or a complicated system are accessed.

**III) CONCEPT:**

The **Facade Pattern** gives you one simple interface to control a complicated system. It hides the system's complexity and handles everything behind the scenes. When you use the facade, it sends your requests to the right parts of the system, but you don’t have to worry about how it works inside.

**IV) PROBLEM IT SOLVES:**

In complex software, there are often many classes, making it hard for the user to understand and use the system. The user needs to know too many details, which makes everything more complicated and tightly connected. The **Facade Pattern** solves this by offering a simple interface that hides all the complex parts, making it easier to work with.

**V) HOW TO RESOLVE:**



* Creating a facade class that provides simple methods which internally call the appropriate subsystems.
*  Hiding the complexity of the system, allowing clients to interact with a single interface without needing to know the subsystem's internal workings.


### **VI) FEATURES**



* **Abstraction**: It hides the internal workings of the subsystem.
* **Simplification**: Provides a simple interface for clients to interact with a complex system.
* **Loose Coupling**: Decouples the client from the subsystem by reducing direct dependencies

**VII) IMPLEMENTATION CODE IN JAVA:**

// Subsystem 1: CPU

class CPU {

    public void start() {

        System.out.println("CPU started.");

    }

    public void shutDown() {

        System.out.println("CPU shut down.");

    }

}

// Subsystem 2: Memory

class Memory {

    public void load(long position, byte[] data) {

        System.out.println("Memory loaded from position: " + position);

    }

}

// Subsystem 3: HardDrive

class HardDrive {

    public byte[] read(long lba, int size) {

        System.out.println("Reading from hard drive...");

        return new byte[size];

    }

}

// Facade class

class ComputerFacade {

    private CPU cpu;

    private Memory memory;

    private HardDrive hardDrive;

    

    public ComputerFacade() {

        this.cpu = new CPU();

        this.memory = new Memory();

        this.hardDrive = new HardDrive();

    }

    

    public void startComputer() {

        cpu.start();

        memory.load(1000, hardDrive.read(500, 1024));

        System.out.println("Computer started.");

    }

    

    public void shutDownComputer() {

        cpu.shutDown();

        System.out.println("Computer shut down.");

    }

}

// Client code

public class FacadePatternExample {

    public static void main(String[] args) {

        ComputerFacade computer = new ComputerFacade();

        computer.startComputer();

        System.out.println("Performing operations...");

        computer.shutDownComputer();

    }

}


Example of Facade Design Pattern:
'''java
@Autowired
private EmployeeFacade employeeFacade;
@PostMapping
public ResponseEntity<String> createEmployee(@Valid @RequestBody Employee employee, BindingResult bindingResult) {
    if (bindingResult.hasErrors()) {
        return ResponseEntity.badRequest().body("Error: " + bindingResult.getFieldError().getDefaultMessage());
    }
    String result = employeeFacade.createEmployee(employee);
    return new ResponseEntity<>(result, HttpStatus.CREATED);
}

@GetMapping("/{id}")
public ResponseEntity<Employee> getEmployeeById(@PathVariable Long id) {
    Employee employee = employeeFacade.getEmployeeById(id);
    if (employee != null) {
        return new ResponseEntity<>(employee, HttpStatus.OK);
    } else {
        return new ResponseEntity<>(HttpStatus.NOT_FOUND);
    }
}



