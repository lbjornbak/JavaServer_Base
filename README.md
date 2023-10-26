# JavaServer_Base
A simple HttpClient class that allows you to make HTTP GET requests to a specified host and port and retrieve the response, including the status code, response headers, and message body. It's a basic implementation of an HTTP client using Java's Socket class for network communication.

A simple HTTPServer using Java's ServerSocket class. The server listens on port 8080 for incoming connections, and when a connection is established, it handles a basic HTTP response.

HttpClient:
  Instance Variables:

  - private final int statusCode; : This variable will store the HTTP status code returned in the response.
  - private final Map<String, String> headerFields = new HashMap<>(); : This Map will store the HTTP response headers as key-value pairs.
  - private String messageBody; : This variable will store the message body of the HTTP response.

  Constructor:

  - public HttpClient(String host, int port, String requestTarget) throws IOException { ... }: This is the constructor of the HttpClient class. It takes three parameters: host (the target host), port (the target port), and       requestTarget (the HTTP request target, typically a path).
  - Inside the constructor, a socket connection to the specified host and port is established using the Socket class.
  - It constructs an HTTP GET request as a string and sends it through the socket's output stream.
  - Then, it reads the response line by line:
    - Parses the status code from the first line of the response.
    - Parses and stores the response headers in the headerFields map.
    - Reads the message body based on the Content-Length header and stores it in the messageBody variable.
    
  Private Helper Methods:

  - private String readBytes(Socket socket, int contentLength) throws IOException { ... }: This method reads the specified number of bytes from the socket's input stream and returns them as a string.
  - static String readLine(Socket socket) throws IOException { ... }: This method reads a line (terminated by '\r\n') from the socket's input stream and returns it as a string.

  Public Getter Methods:

  - public int getStatusCode() : Returns the HTTP status code.
  - public String getHeader(String headerName) : Returns the value of a specific response header based on its name.
  - public int getContentLength() : Returns the content length specified in the Content-Length header.
  - public String getMessageBody() : Returns the message body of the HTTP response.

HttpServer:
  - ServerSocket named serverSocket is created, which listens on port 8080 for incoming connections.

  Accepting Client Connection:
  - Socket clientSocket = serverSocket.accept();: This line blocks until a client connects to the server. When a client connection is established, a new Socket named clientSocket is created to handle communication with        that client.
    
  Reading HTTP Request:
  - String requestLine = HttpClient.readLine(clientSocket);: This code calls the readLine method from the HttpClient class to read the first line of the HTTP request sent by the client, which typically contains the            request method, request target (URL), and HTTP version.
  - It then prints the request line to the console.

  Reading HTTP Request Headers:
  - The code enters a loop to read and print each header line sent by the client until it encounters a blank line, which indicates the end of the headers:

  Creating and Sending HTTP Response:
  - The code prepares an HTTP response message with a simple "Hello world" message in the message body.

  Sending the Response:
  - clientSocket.getOutputStream().write(responseMessage.getBytes()); : This code sends the HTTP response message back to the client by writing it to the client's socket output stream.

  Server Termination:
  - The code in this example doesn't include a server termination mechanism, so the server will run indefinitely until it is manually terminated or the program is forcibly stopped.

  Responses:
  - HttpServer should respond with 404
  - HttpServer should include request target in 404 -
  - Return a static content for /hello
  - Content-type
  - Return HTML file from disk
   
    Return:
  - Process GET request for form
  - Process POST request from form