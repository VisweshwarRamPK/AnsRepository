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