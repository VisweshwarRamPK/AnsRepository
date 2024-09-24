**16) JASPER REPORT EXECUTION IN JAVA:**


#### **I) Definition:**



* **JasperReports is a Java library used to generate reports in various formats like PDF, Excel, and HTML. Reports are designed using tools (e.g., JasperSoft Studio) and generated in Java applications.**

**II) Steps to Execute Jasper Reports in Java:**

**Step 1: Load the Report Template**



* **The first step involves loading and compiling the report design template (.jrxml file) into a JasperReport object.**

**Code: \
JasperReport jasperReport = JasperCompileManager.compileReport("path/to/report.jrxml");**



* **Definition:**
    * **JasperCompileManager.compileReport(): Compiles the .jrxml file (report design in XML) into a binary format that JasperReports can use.**

**Step 2: Provide Data**



* **Once the report is compiled, you fill it with data. This data can come from a database (e.g., MySQL) or Java objects (JavaBeans).**

**Code: \
Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/db", "user", "password");**

**JasperPrint jasperPrint = JasperFillManager.fillReport(jasperReport, null, conn);**



* **Definition:**
    * **DriverManager.getConnection(): Establishes a connection to a database.**
    * **JasperFillManager.fillReport(): Fills the compiled Jasper report (jasperReport) with data from the database (conn).**

**Step 3: Export the Report**



* **After filling the report with data, you can export it to a format like PDF, HTML, etc.**

**Code: \
JasperExportManager.exportReportToPdfFile(jasperPrint, "output/report.pdf");**



* **Definition:**
    * **JasperExportManager.exportReportToPdfFile(): Exports the filled report (jasperPrint) to a PDF file at the specified path ("output/report.pdf").**