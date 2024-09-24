**14) JSP:**

**JAVA SERVER PAGES(JSP):**

**I) DEFINITION:**

JSP stands for JavaServer Pages, a server-side technology used to create dynamic web content by embedding Java code in HTML pages.JSP pages are compiled into Servlets, and then they are executed on the server to produce dynamic content for the client.

**II) DIFFERENCE BETWEEN JSP AND SERVLETS:**

JSP is more convenient when dealing with HTML-heavy content and a bit of java code, while Servlets are Pure Java classes that handle HTTP requests and generate responses programmatically.

**III) LIFE CYCLE OF A JSP PAGE:**

**Translation:** JSP files are converted into a Servlet by the JSP engine.

**Compilation: **The generated Servlet is compiled into bytecode.

**Execution:** The compiled Servlet is executed, and dynamic content is generated.

**Destruction: **The JSP is removed from memory when no longer in use.

**IV) JSP DIRECTIVES:**

These are instructions to the JSP engine on how to process the page. The key directives are:

**<code>&lt;%@ page %></code></strong>: Defines page-specific attributes like contentType, errorPage, etc.

**<code>&lt;%@ include %></code></strong>: Used to include other files (static or dynamic).

**<code>&lt;%@ taglib %></code></strong>: Declares a custom tag library for the JSP page.

**V) JSP SCRIPTING ELEMENTS:**

These are used to embed Java code into JSP:

**Declarations (<code>&lt;%! ... %></code>)</strong>: Used to declare variables and methods in JSP.

**Scriptlets (<code>&lt;% ... %></code>)</strong>: Embeds Java code directly into the HTML page.

**Expressions (<code>&lt;%= ... %></code>)</strong>: Outputs the value of a Java expression to the client.

**VI) IMPLICIT OBJECTS IN JSP:**

**These are objects provided by the JSP engine that you can use without explicitly declaring them. Common ones include:**


```
request, response, session, application, out, config
```


**VII) JSP ACTIONS:**

**JSP actions are XML-like tags that perform certain tasks like**

**<code>&lt;jsp:include></code>: includes content at request time.</strong>

**<code>&lt;jsp:forward></code>: Forwards a request to another resource (like another JSP or Servlet).</strong>

**<code>&lt;jsp:param></code>: Passes parameters between resources</strong>

**VIII) CUSTOM TAGS AND TAG LIBRARIES:**

Custom tags are used to extend the functionality of JSP by writing reusable components. These are usually bundled in tag libraries.

**IX) JAVA EXPRESSION LANGUAGE(EL):**

EL simplifies access to data stored in JavaBeans, request parameters, or session attributes.

**X) ERROR HANDLING IN JSP:**

JSP allows specifying error pages using the `errorPage` attribute in the `&lt;%@ page %>` directive.

**XI)PROBLEMS SOLVED BY JSP:**


### **Mixing Java Code with HTML**



* **Problem**: Before JSP, developers used Java Servlets to generate HTML content dynamically. However, this involved writing large blocks of HTML code inside Java classes, which quickly became unmanageable and hard to maintain, especially for complex pages. Mixing presentation (HTML) with business logic (Java) in Servlets led to tightly coupled, hard-to-read code.
* **How JSP solves this**: JSP allows developers to embed Java code directly within HTML using special tags (`&lt;% %>`). This separation of concerns improves the clarity and maintainability of the code. HTML designers can focus on presentation, while Java developers handle business logic, making collaboration easier.


### **Difficult Maintenance and Scalability of Servlets**



* **Problem**: As applications grow, maintaining Servlets that handle both logic and presentation becomes increasingly difficult. Every change to the UI required modifying Java code, recompiling it, and redeploying it. This slows down the development process and introduces bugs.
* **How JSP solves this**: JSP separates presentation from business logic by allowing the use of JavaBeans, custom tags, and the Model-View-Controller (MVC) architecture. JSP pages handle the presentation (view), while Servlets or JavaBeans manage the logic (controller and model). This modular approach makes applications more maintainable and scalable.


### **Tight Coupling Between UI and Backend Code**



* **Problem**: In early web development using Servlets, UI code (HTML) was often intermingled with backend code (Java). This made it difficult to maintain or update the front-end design without affecting the backend logic.
* **How JSP solves this**: JSP promotes a clearer separation between front-end (view) and back-end (model/controller) by encouraging the use of JavaBeans and custom tags. JSP can invoke these components without embedding significant Java code directly in the HTML, allowing developers to update the UI without rewriting backend logic.