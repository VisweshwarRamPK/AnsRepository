**8) CACHE:**

**I) DEFINITION:**

**Caching** is a performance optimization technique used to store copies of frequently accessed data in a location that can be quickly retrieved, improving response times. The primary goal is to improve performance by avoiding repeated access to slower data stores, like databases or external APIs.

**II) CACHE USE:**

**Performance improvement: **Cache provides quick access to frequently used data.

**Reduced load on backend systems: **It reduces the number of expensive calls to databases, APIs, or disk storage.It helps to reduce the load on backend systems.

**Lower latency**: It minimizes data access times, which improves the response time for users.

**III) TYPES OF CACHE:**

**Client-side cache**:  Data is stored on the client side (e.g., browser,local repository)

**Server-side cache**: Data is stored on the server side.(e.g:Redis and Memcached.)

**Distributed cache**: A cache that is shared across multiple servers to avoid single points of failure (e.g., Redis, Memcached clusters).

**IV) CACHE STRATEGIES:**


#### **Cache Aside (Lazy Loading)**



* **How it works:**
    * **The application first checks if the needed data is in the cache.**
    * **If the data is not there (called a cache miss), it retrieves the data from the database or another source.**
    * **Once it has the data, it stores it in the cache for future use and serves the data to the user.**
    * **The cache is only updated when the data is actually needed, which saves resources.**


#### **Write Through**



* **How it works:**
    * **Whenever new data is added or existing data is updated, the system writes the data to both the cache and the database at the same time.**


#### **Write Back (Write Behind)**



* **How it works:**
    * **New or updated data is written to the cache first, but it’s only written to the database later in the background.Since the system writes to the cache first, the process is faster for users.**

**V) CACHE EVICTION POLICIES:**

**Least Recently Used (LRU):** Removes the least recently accessed items when the cache is full.

**Least Frequently Used (LFU):** Removes the items that are accessed the least number of times.

**First-In-First-Out (FIFO):** Removes the oldest items based on when they were added to the cache.

**Time-to-Live (TTL):** Cache entries have an expiration time, and they are removed once this time is reached.

**VI) CACHE TOOLS AND FRAMEWORKS:**

**Redis: **An key value cashing system that supports a wide range of data structures such as list,set etc

**Memcached:** A distributed caching system, known for its simplicity and speeding up dynamic web applications.

**CDNs (Content Delivery Networks):** Cloudflare, AWS CloudFront—used to cache static content geographically closer to users to reduce latency.

**Spring cache: **It allows easy integration of various cache providers like redis,memcached in java applications.

**VII) PROBLEMS SOLVED BY CACHE:**



* Reduces latency by providing faster access to frequently used data.
* Decreases load on backend systems like databases and APIs by serving cached data,and also helps in cost efficiency.
* Improves scalability by offloading traffic from backend services.
* Minimizes network latency by caching data closer to the user (CDN)

**VIII) COMMON USE CASE FOR CACHING:**

**Database Query Caching**: Store results of frequent database queries to reduce load and response times.


### **IX) Cache Performance Considerations**



* **Hit Ratio**: This is a key metric that measures the percentage of requests served by the cache. A high hit ratio means the cache is being used effectively.
Implemenation of Simple Inmemory Cache:
  ```java
    private final Map<Long, Employee> employeeCache = new ConcurrentHashMap<>();

    public Employee getEmployeeById(Long id) {

        Employee cachedEmployee = employeeCache.get(id);
        if (cachedEmployee != null) {
            System.out.println("Returning employee from cache: " + id);
            return cachedEmployee;
        }


        System.out.println("Cache miss. Fetching employee from database for ID: " + id);
        Employee employee = employeeRepository.getEmployeeById(id);
        if (employee != null) {
            employeeCache.put(id, employee);
        }
        return employee;
    }
