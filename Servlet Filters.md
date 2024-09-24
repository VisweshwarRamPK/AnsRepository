20) SERVLET FILTERS:
I) DEFINITION:
 Servlet filters are objects that intercept requests and responses in a Java web application. They process incoming requests before they reach a servlet and outgoing responses before they are sent to the client.
II) PURPOSE:
Pre-processing and Post-processing: Filters allow you to perform actions both before the request reaches the servlet and after the response leaves the servlet.
Example: Filters can be used for logging, authentication, input validation.
III) PROBLEMS SOLVED BY SERVLET FILTERS:
Handling Common Tasks Across Multiple Servlets:
      * Problem: Tasks like logging, authentication, and error handling need to be applied to many parts of your application.
      * Solution: Filters handle these tasks in one place, making it easier to apply them everywhere needed.
Request and Response Modification:
      * Problem: There may be a need to modify incoming requests or outgoing responses, such as adding headers, handling encoding, or compressing output.
      * Solution: Filters can adjust the request before it reaches the servlet or modify the response before it goes back to the user.
Authentication and Authorization:
      * Problem: Ensuring that only authorized users can access certain resources.
      * Solution: Filters can intercept requests to check user credentials (such as a token or session) before allowing access to a servlet.
Logging and Monitoring:
      * Problem: Tracking all requests and responses can be hard if you have many servlets.
      * Solution: Filters can log every request and response in one place, making it easier to monitor your application.
Error Handling:
      * Problem: Handling errors consistently across servlets can be difficult.
      * Solution:  Filters can catch errors and redirect users to a common error page, simplifying error handling.
IV)HOW SERVLET FILTERS DIFFERS FROM SERVLETS:
Filters: It doesn't directly handle the request and response.Pre-process or post-process requests/responses .
Servlets: Directly handle the request and generate the response content.
V) LIFE CYCLE OF SERVLET FILTERS:
      * Initialization: The filter is initialized once when the web application starts (init() method).
      * Filtering: For each request, the filter’s doFilter() method is called, where it can modify or inspect the request/response.
      * Destruction: When the web application shuts down, the filter is destroyed (destroy() method).
VI) FEATURES OF SERVLET FILTERS:
Chaining: Multiple filters can be chained together, meaning that a request/response passes through all the filters in a predefined order before it reaches the servlet.
Declarative Configuration: Filters can be configured in the web.xml or annotated with @WebFilter
Reusability: Once a filter is created, it can be reused across multiple servlets 


VII) USE OF SERVLET FILTERS:


Request and Response Modification:
      * Purpose: Filters can modify incoming requests and outgoing responses. This includes adding headers, adjusting encoding, or compressing content.
      * Use Case: A filter could be used to add security headers to all responses or to compress HTML responses for faster delivery.
. Authentication and Authorization:
      * Purpose: Filters can handle user authentication and authorization, ensuring that only authorized users can access certain resources.
      * Use Case: A filter can check if a user is logged in or has the right permissions before allowing access to a protected resource
Logging and Monitoring:
      * Purpose: Filters can be used to log details of requests and responses,
Error Handling:
      * Purpose: Filters can handle exceptions and errors consistently across your application, reducing code duplication.
      * Use Case: A filter can catch exceptions thrown by servlets, log the error, and redirect users to a custom error page, ensuring consistent error handling.


Enhancing Performance:
      * Purpose: Filters can optimize performance by caching responses or compressing data.
      * Use Case: A filter might cache frequently requested data to reduce database load or compress response data to save bandwidth.
VIII) COMPONENTS:
Filter Interface: The main interface defines the core methods (init(), doFilter(), and destroy()) that filters use to intercept and process requests/responses.
Filter chain: Represents the sequence of filters applied to a request/response. The FilterChain object is used within the doFilter() method to pass the request and response to the next filter or the target servlet. Enables multiple filters to be applied in sequence, creating a processing pipeline.