
**19) SPRING SECURITY:**

**I) DEFINITION:**



* Spring Security is a framework that provides authentication, authorization, and other security features to protect Java applications.
* It ensures that only authorized users can access certain parts of your application and protects against common security threats.

**II) FEATURES:**

**Authentication:**



* **Definition: **Verifies the identity of users (i.e., making sure they are who they say they are).
* **How It Works: **Users provide credentials (like username and password) which are checked against a user store (like a database). If credentials are correct, the user is authenticated.

**Authorization:**



* **Definition:** Determines what authenticated users are allowed to do (i.e., what resources they can access and what actions they can perform).
* **How It Works: **Based on user roles and permissions, Spring Security restricts access to different parts of the application.

**Secure Communication:**



* **Definition: **Protects data in transit to ensure that communication between the client and server is secure.
* **How It Works: **Configures HTTPS to encrypt data exchanged between the client and server.

**CSRF (Cross-Site Request Forgery):**



* **What it is: **An attack where a bad website tricks your browser into making an unwanted request to another site where you’re logged in.
* **How Spring Security Helps:** It uses special tokens in forms. These tokens are like secret codes that confirm the request is coming from a legitimate source. If the code doesn’t match, the request is blocked.

**XSS (Cross-Site Scripting):**



* **What it is: **An attack where malicious scripts are injected into web pages, potentially stealing user data or performing unwanted actions.
* **How Spring Security Helps: **It “sanitizes” user input which helps prevent harmful scripts from being run.

**Secure Password Storage: **Use strong hashing algorithms (like BCrypt) to store passwords securely.

**III) COMMON SECURITY CONFIGURATIONS:**

**Basic Authentication:**



* **Definition: A simple authentication method where credentials are username and password.**

**Form-Based Authentication:**



* **Definition: A web form is used for users to log in.**
* **How It Works: Provides a login page where users enter their credentials. After successful login, users are redirected to the protected resources.**

**OAuth2 / JWT (JSON Web Tokens):**



* **Definition: Modern protocols for authentication and authorization.**
* **Oauth2 is used for delegated authentication and JWT for stateless authentication.**

**IV) COMPONENTS:**

**Authentication:**

Authentication is the process of verifying the identity of a user or system.

**Components involved:**



* **Authentication Manager: **This component handles the authentication process. It checks if the user’s credentials (like username and password) are valid.
* **Authentication Provider:** A system that validates user credentials (like username and password).by an external service like LDAP,OAuth2.
* **UserDetailsService: **A service that loads information about the user’s username,password and role.
* **PasswordEncoder: **Responsible for encoding and validating passwords (e.g., `BCryptPasswordEncoder`).


### **Authorization:**

After successful authentication, authorization determines what actions or resources the user is allowed to access.

**Access Control**: Defines what resources the authenticated user can access. It can be role-based access control.

**Security Filter Chain:**

Spring Security uses a chain of filters to process security logic. Some of the common filters:



* UsernamePasswordAuthenticationFilter: Handles login requests with a username and password.
* JwtAuthenticationFilter (custom): Filters for JWT-based authentication in stateless applications.


### **OAuth2 and JWT Support:**

Spring Security also supports OAuth2 for delegated authentication (e.g., using Google, Facebook) and JWT (JSON Web Token) for stateless authentication, where tokens are used to maintain user state without sessions.

**V)USE OF SPRING SECURITY:**



* Protects web applications

**VI)PROBLEMS SOLVED BY SPRING SECURITY:**

**Authentication and Authorization: **Manages both who users are and what they can do.

**Security Against Web Attacks: **Protects applications from CSRF, XSS,  and more.

**Session Management:** Secures user sessions to prevent attacks like hijacking.

**Password Security: **Safely stores and manages user credentials by using BCRYPT.
