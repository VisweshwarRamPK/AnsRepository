**6)ETL SCENARIO:**


#### **I) Reading a File from FTP/SFTP Server**



* **Scenario: **Downloading a file from an FTP or SFTP server.
* **Steps:**
    1. Connect to the server using credentials (hostname, username, password/SSH key).
    2. Navigate to the directory where the file is stored.
    3. Download the file to your local system using an FTP/SFTP client.

**FTP Example Code:**

FTPClient ftpClient = new FTPClient();

ftpClient.connect("ftp.example.com");

ftpClient.login("username", "password");

String remoteFile = "/remote/path/file.txt";

FileOutputStream outputStream = new FileOutputStream("local/path/file.txt");

ftpClient.retrieveFile(remoteFile, outputStream);

outputStream.close();

ftpClient.logout();

**SFTP Example Code:**

JSch jsch = new JSch();

Session session = jsch.getSession("username", "sftp.example.com", 22);

session.setPassword("password");

session.setConfig("StrictHostKeyChecking", "no");

session.connect();

ChannelSftp channelSftp = (ChannelSftp) session.openChannel("sftp");

channelSftp.connect();

FileOutputStream outputStream = new FileOutputStream("local/path/file.txt");

channelSftp.get("/remote/path/file.txt", outputStream);

outputStream.close();

channelSftp.disconnect();

session.disconnect();


#### **II) Writing a File to FTP/SFTP Server**



* **Scenario:** Uploading a file from your local system to an FTP or SFTP server.
* **Steps:**
    1. **Connect to the server** using credentials.
    2. **Navigate** to the directory where the file should be uploaded.
    3. **Upload** the file from your local system to the server.

**FTP Example Code:**

FTPClient ftpClient = new FTPClient();

ftpClient.connect("ftp.example.com");

ftpClient.login("username", "password");

FileInputStream inputStream = new FileInputStream(new File("local/path/file.txt"));

ftpClient.storeFile("/remote/path/file.txt", inputStream);

inputStream.close();

ftpClient.logout();

**SFTP Example Code:**

JSch jsch = new JSch();

Session session = jsch.getSession("username", "sftp.example.com", 22);

session.setPassword("password");

session.setConfig("StrictHostKeyChecking", "no");

session.connect();

ChannelSftp channelSftp = (ChannelSftp) session.openChannel("sftp");

channelSftp.connect();

FileInputStream inputStream = new FileInputStream("local/path/file.txt");

channelSftp.put(inputStream, "/remote/path/file.txt");

inputStream.close();

channelSftp.disconnect();

session.disconnect();
