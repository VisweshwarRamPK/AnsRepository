Validation:

Validation in EmployeeController:

```java
@PostMapping
public ResponseEntity<String> createEmployee(@Valid @RequestBody Employee employee, BindingResult bindingResult) {
    if (bindingResult.hasErrors()) {
        return ResponseEntity.badRequest().body("Error: " + bindingResult.getFieldError().getDefaultMessage());
    }
    String result = employeeService.createEmployee(employee);
    return new ResponseEntity<>(result, HttpStatus.CREATED);
}

@PutMapping("/{id}")
public ResponseEntity<String> updateEmployee(@PathVariable Long id, @Valid @RequestBody Employee employee, BindingResult bindingResult) {
    if (bindingResult.hasErrors()) {
        return ResponseEntity.badRequest().body("Error: " + bindingResult.getFieldError().getDefaultMessage());
    }
    String result = employeeService.updateEmployee(id, employee);
    return new ResponseEntity<>(result, HttpStatus.OK);
}
```

Validation in Employee Model
```java
@NotNull(message = "Name is required")
@Size(min = 2, max = 100, message = "Name must be between 2 and 100 characters")
private String name;

@NotNull(message = "Position is required")
@Size(min = 2, max = 50, message = "Position must be between 2 and 50 characters")
private String position;

@Min(value = 0, message = "Salary must be positive")
private double salary;
```
