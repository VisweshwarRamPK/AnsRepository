**7) PARSING:**

**I)JSON II)XML**

**I)JSON:**

We can use the **Jackson** library to convert JSON data into Java objects.

**CODE:**

 ObjectMapper objectMapper = new ObjectMapper();

        // Read JSON file and convert it to MyClass object

        MyClass obj = objectMapper.readValue(new File("data.json"), MyClass.class);

        System.out.println(obj.getName() + " is " + obj.getAge() + " years old.");

**MYCLASS:**

class MyClass {

    private String name;

    private int age;

    public String getName() { return name; }

    public void setName(String name) { this.name = name; }

    public int getAge() { return age; }

    public void setAge(int age) { this.age = age; }

}

**II) XML:**

 Unmarshalling is a process used in **JAXB** (Java Architecture for XML Binding) that is commonly used to convert XML data into Java objects.

**CODE:**

JAXBContext context = JAXBContext.newInstance(Employee.class);

Unmarshaller unmarshaller = context.createUnmarshaller();

// Convert XML to Java object

Employee employee = (Employee) unmarshaller.unmarshal(new File("employee.xml"));

Example of JSON to XML Parsing:
```java

@PostMapping("/convert")
public ResponseEntity<String> convertJsonToXml(@RequestBody String json) {
    try {
        JsonToXmlConverter converter = new JsonToXmlConverter();
        String xml = converter.convertJsonToXml(json);
        return ResponseEntity.ok(xml);
    } catch (IOException e) {
        return ResponseEntity.badRequest().body("Error converting JSON to XML: " + e.getMessage());
    }
}

```
Example of XML to JSON Parsing:
```java

@PostMapping("/convert/xml")
public ResponseEntity<String> convertXmlToJson(@RequestBody String xml) {
    try {
        JsonToXmlConverter converter = new JsonToXmlConverter();
        String json = converter.convertXmlToJson(xml);
        return ResponseEntity.ok(json);
    } catch (IOException e) {
        return ResponseEntity.badRequest().body("Error converting XML to JSON: " + e.getMessage());
    }
}

