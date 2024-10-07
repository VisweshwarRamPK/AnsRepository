**23)JUNIT5:**

**I) DEFINITION:**

**JUnit 5 is the latest version of the JUnit testing framework used for writing and executing unit testing in Java.**

**JAVA WITH JDBC CONNECTION PROGRAM:**

**import java.sql.Connection;**

**import java.sql.DriverManager;**

**import java.sql.SQLException;**

**public class DatabaseConnection {**

**    private static final String URL = "jdbc:mysql://localhost:3306/mydb";**

**    private static final String USER = "root";**

**    private static final String PASSWORD = "password";**

**    public Connection getConnection() throws SQLException {**

**        return DriverManager.getConnection(URL, USER, PASSWORD);**

**    }**

**    public static void main(String[] args) {**

**        DatabaseConnection dbConnection = new DatabaseConnection();**

**        try {**

**            Connection connection = dbConnection.getConnection();**

**            if (connection != null) {**

**                System.out.println("Connection successful!");**

**            }**

**        } catch (SQLException e) {**

**            System.out.println("Failed to connect to the database.");**

**            e.printStackTrace();**

**        }**

**    }**

**}**

**JUNIT TEST WITH MOCKITO:**

**import org.junit.jupiter.api.BeforeEach;**

**import org.junit.jupiter.api.Test;**

**import org.mockito.Mockito;**

**import java.sql.Connection;**

**import java.sql.DriverManager;**

**import java.sql.SQLException;**

**import static org.junit.jupiter.api.Assertions.*;**

**import static org.mockito.Mockito.*;**

**class DatabaseConnectionTest {**

**    private DatabaseConnection dbConnection;**

**    @BeforeEach**

**    void setUp() {**

**        dbConnection = new DatabaseConnection();**

**        Mockito.mockStatic(DriverManager.class); // Mock DriverManager once for all tests**

**    }**

**    @Test**

**    void testGetConnectionSuccess() throws SQLException {**

**        // Mock successful connection**

**        Connection mockConnection = mock(Connection.class);**

**        when(DriverManager.getConnection(anyString(), anyString(), anyString())).thenReturn(mockConnection);**

**        // Verify connection is not null**

**        assertNotNull(dbConnection.getConnection());**

**    }8**

**   @Test**

**    void testGetConnectionFailure() throws SQLException {**

**        // Mock connection failure**

**        when(DriverManager.getConnection(anyString(), anyString(), anyString())).thenThrow(new SQLException("Failed to connect"));**

**        // Verify exception is thrown**

**        assertThrows(SQLException.class, dbConnection::getConnection);**

**    }**

Example of Junit5:

---java
package com.example.employee.model;

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

public class EmployeeTest {
    private Employee employee;

    @BeforeEach
    public void setUp() {
        employee = new Employee("1", "John Doe", "Engineering", 75000.00);
    }

    @Test
    public void testEmployeeConstructorAndGetters() {
        assertEquals("1", employee.getId());
        assertEquals("John Doe", employee.getName());
        assertEquals("Engineering", employee.getDepartment());
        assertEquals(75000.00, employee.getSalary());
    }

    @Test
    public void testDefaultConstructor() {
        Employee defaultEmployee = new Employee();
        // Check that the default values are null or 0.0
        assertNull(defaultEmployee.getId());
        assertNull(defaultEmployee.getName());
        assertNull(defaultEmployee.getDepartment());
        assertEquals(0.0, defaultEmployee.getSalary());
    }

    @Test
    public void testSetters() {
        employee.setId("2");
        employee.setName("Jane Doe");
        employee.setDepartment("HR");
        employee.setSalary(85000.00);
        assertEquals("2", employee.getId());
        assertEquals("Jane Doe", employee.getName());
        assertEquals("HR", employee.getDepartment());
        assertEquals(85000.00, employee.getSalary());
    }
}
