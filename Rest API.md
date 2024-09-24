**1) IMPLEMENT A REST API IN JAVA **

**I)PUBLISH SCENARIO II)CONSUME SCENARIO**

**I)PUBLISH SCENARIO:**

**Step 1: Create a Spring Boot Project**

Use Spring Initializr with dependencies like Spring Web.

**Step 2: Define a Controller**

@RestController

@RequestMapping("/api")

public class SimpleController {

    @GetMapping("/message")

    public ResponseEntity&lt;String> getMessage() {

        return new ResponseEntity&lt;>("Hello from REST API!", HttpStatus.OK);

    }

    @PostMapping("/message")

    public ResponseEntity&lt;String> postMessage(@RequestBody String message) {

        return new ResponseEntity&lt;>("You posted: " + message, HttpStatus.CREATED);

    }

}

**Step 3: Run the Application \
**Run the app and access the API at <code>[http://localhost:8080/api/message](http://localhost:8080/api/message)</code>.

**II)CONSUME SCENARIO**

**Step 1: Add Dependencies**

Ensure Spring Web dependencies are included in `pom.xml`.

**Step 2: Create a RestTemplate Bean**

@Configuration

public class RestTemplateConfig {

    @Bean

    public RestTemplate restTemplate() {

        return new RestTemplate();

    }

}

**Step 3: Create a Service to Consume External API**

@Service

public class ApiService {

    private final RestTemplate restTemplate;

    public ApiService(RestTemplate restTemplate) {

        this.restTemplate = restTemplate;

    }

    public String consumeExternalApi() {

        String apiUrl = "https://jsonplaceholder.typicode.com/posts/1";

        return restTemplate.getForObject(apiUrl, String.class);

    }

}

**Step 4: Create a Controller to Call the Service**

@RestController

@RequestMapping("/consume")

public class ConsumeController {

    private final ApiService apiService;

    public ConsumeController(ApiService apiService) {

        this.apiService = apiService;

    }

    @GetMapping("/external")

    public ResponseEntity&lt;String> getExternalData() {

        String response = apiService.consumeExternalApi();

        return new ResponseEntity&lt;>(response, HttpStatus.OK);

    }

}

**Step 5: Run the Application**

Access the API at <code>[http://localhost:8080/consume/external](http://localhost:8080/consume/external)</code>.