Implementation of Logging:

Logging in EmployeeController
```java
private static final Logger logger = LoggerFactory.getLogger(EmployeeController.class);

@GetMapping
public ResponseEntity<List<Employee>> getAllEmployees() {
    logger.info("Fetching all employees");
    List<Employee> employees = employeeService.findAll();
    return ResponseEntity.ok(employees);
}

@GetMapping("/{id}")
public ResponseEntity<Employee> getEmployeeById(@PathVariable String id) {
    logger.info("Fetching employee with id: {}", id);
    Employee employee = employeeService.findById(id);
    return ResponseEntity.ok(employee);
}

@PostMapping
public ResponseEntity<Employee> createEmployee(@RequestBody Employee employee) {
    logger.info("Creating new employee: {}", employee);
    Employee savedEmployee = employeeService.save(employee);
    return ResponseEntity.ok(savedEmployee);
}

@PutMapping("/{id}")
public ResponseEntity<Employee> updateEmployee(@PathVariable String id, @RequestBody Employee employee) {
    logger.info("Updating employee with id: {}", id);
    Employee updatedEmployee = employeeService.update(id, employee);
    return ResponseEntity.ok(updatedEmployee);
}

@DeleteMapping("/{id}")
public ResponseEntity<Void> deleteEmployee(@PathVariable String id) {
    logger.info("Deleting employee with id: {}", id);
    employeeService.delete(id);
    return ResponseEntity.noContent().build();
}
```
Logging in EmployeeService
```java

private static final Logger logger = LoggerFactory.getLogger(EmployeeService.class);

public List<Employee> findAll() {
    logger.info("Retrieving all employees");
    return employeeRepository.findAll();
}

public Employee findById(String id) {
    logger.info("Searching for employee with id: {}", id);
    return employeeRepository.findById(id)
        .orElseThrow(() -> {
            logger.error("Employee with id: {} not found", id);
            return new EmployeeNotFoundException(id);
        });
}

public Employee save(Employee employee) {
    logger.info("Saving employee: {}", employee);
    return employeeRepository.save(employee);
}

public Employee update(String id, Employee employee) {
    logger.info("Updating employee with id: {}", id);
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
}

public void delete(String id) {
    logger.info("Deleting employee with id: {}", id);
    employeeRepository.findById(id)
        .ifPresentOrElse(
            existingEmployee -> {
                logger.info("Employee found. Deleting employee with id: {}", id);
                employeeRepository.deleteById(id);
            },
            () -> {
                logger.error("Employee with id: {} not found for deletion", id);
                throw new EmployeeNotFoundException(id);
            }
        );
}
