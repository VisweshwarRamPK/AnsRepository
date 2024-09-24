
**17. FTP/SFTP - SPRING INTEGRATION**

**I) WORKFLOW:**

**Message Source (Inbound Channel Adapter):**



* **Inbound channel adapter connects to an FTP/SFTP server to fetch files.**
* **It uses polling to check the remote directory periodically for new files.**
* **When a file is found, it is retrieved and converted into a message.**

**Message Channel:**



* **Files are passed through a message channel like a conveyor belt.**
* **The message includes the file's content and metadata (e.g., file name, size).**

**Filters (Optional):**



* **You can filter files based on criteria (e.g., process only <code>.txt</code> files).</strong>
* <strong>Filters ensure only relevant files are processed, reducing unnecessary load.</strong>

<strong>Message Transformation (Optional):</strong>



* **If necessary, the message content can be transformed (e.g., converting CSV data).**
* **You can apply business logic to process the message before it moves forward.**

**Message Destination (Outbound Channel Adapter):**



* **The final step sends the processed message back to the FTP/SFTP server.**
* **The outbound channel adapter uploads the file to the desired server location.**

**II) CODE IMPLEMENTATION:**

**Inbound Channel Adapter (SFTP File Fetching):**



* **Configuration class:**

**@Configuration**

**@EnableIntegration**

**public class SftpIntegrationConfig {**

**    @Bean**

**    public SessionFactory&lt;LsEntry> sftpSessionFactory() {**

**        DefaultSftpSessionFactory factory = new DefaultSftpSessionFactory(true);**

**        factory.setHost("sftp-server.com");**

**        factory.setPort(22);**

**        factory.setUser("username");**

**        factory.setPassword("password");**

**        return factory;**

**    }**

**    @Bean**

**    public IntegrationFlow sftpInboundFlow() {**

**        return IntegrationFlows**

**            .from(Sftp.inboundAdapter(sftpSessionFactory())**

**                    .remoteDirectory("/remote/dir/")**

**                    .localDirectory(new File("local-dir"))**

**                    .autoCreateLocalDirectory(true)**

**                    .deleteRemoteFiles(false),**

**                e -> e.poller(Pollers.fixedDelay(5000)))**

**            .channel("fileInputChannel")**

**            .get();**

**    }**

**}**

**Explanation:**



* **SftpSessionFactory: Establishes an SFTP session using server credentials.**
* **Sftp.inboundAdapter: Fetches files from a remote directory and downloads them to a local directory.**
* **Polling: Polls the SFTP server every 5 seconds for new files.**
* **Channel: Files are passed to the <code>fileInputChannel</code> for further processing.</strong>

<strong>Message Channel:</strong>



* **Configuration class**

**@Configuration**

**public class MessageChannelConfig {**

**    @Bean**

**    public MessageChannel fileInputChannel() {**

**        return new DirectChannel();**

**    }**

**    @Bean**

**    public MessageChannel fileProcessingChannel() {**

**        return new DirectChannel();**

**    }**

**}**

**Explanation:**



* **Message Channels: Defines channels for communication between system components.**
* **<code>fileInputChannel</code>: Handles files fetched from the SFTP server.</strong>
* <strong><code>fileProcessingChannel</code>: Processes the fetched files before they are sent further.</strong>

<strong>Outbound Channel Adapter (Uploading Processed Files):</strong>



* **Configuration class:**

**@Configuration**

**public class SftpOutboundConfig {**

**    @Bean**

**    public IntegrationFlow sftpOutboundFlow() {**

**        return IntegrationFlows.from("fileProcessingChannel")**

**            .handle(Sftp.outboundAdapter(sftpSessionFactory())**

**                    .remoteDirectory("/remote/output/dir/"))**

**            .get();**

**    }**

**}**



* **Explanation:**
    * **Sftp.outboundAdapter: Uploads processed files to a remote SFTP directory.**
    * **Integration Flow: Files from <code>fileProcessingChannel</code> are uploaded to <code>/remote/output/dir/</code>.</strong>
