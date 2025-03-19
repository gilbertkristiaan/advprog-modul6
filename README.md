# Gilbert Kristian - Adpro A - 2306274951

## Milestone 1: Single-Threaded Web Server  

In creating a single-threaded web server, two main protocols are involved: **Hypertext Transfer Protocol (HTTP)** and **Transmission Control Protocol (TCP)**. The fundamental principle of these protocols follows a **request-response** model, where the server receives and responds to client requests.  

- **TCP** is a low-level protocol that defines how data is transmitted between servers but does not specify the content of the data.  
- **HTTP** determines the structure of request and response messages. The data from HTTP is transmitted over TCP.  

Initially, the program can only receive browser connection requests using `TcpListener` bound to `127.0.0.1:7878`. Each time a connection is received, the program prints **"Connection established!"**.  

## Function Explanations  

- **`bind()`**: Connects `TcpListener` to a specific address and port on the local machine to listen for incoming connections.  
- **`unwrap()`**: Extracts the value from a `Result` or `Option`. If the value is `Ok` or `Some`, it returns the contained value. If it is `Err` or `None`, `unwrap()` causes the program to panic and terminate, indicating a critical error.  
- **`incoming()`**: Receives incoming connections on `TcpListener`, returning an iterator that produces `Result<TcpStream, Error>`. Each element in the iterator represents an open connection between the client and the server. Connections are handled sequentially.  

## Handling Requests  

To manage how the server responds to browser requests, the `handle_connection()` function is implemented.  

- The console prints the **HTTP request** at the end of the method.  
- `BufReader` reads the stream or lines from `TcpStream` using the `.lines()` method.  
- The **http_request** variable collects the HTTP request lines received from the browser.  


## Milestone 2: Returning HTML
Screenshot : 
![screenshot](/assets/images/commit_html.png)

In this milestone, the **`handle_connection`** function is enhanced to return an HTML response. This is done by reading an HTML file from disk and sending its contents as part of the server's response.  

## Implementation Details  

- The function uses **`fs::read_to_string`** to load the contents of `hello.html` into a String. This allows the server to send structured HTML content to the client.  
- A proper HTTP response is then crafted, starting with the **status line** `"HTTP/1.1 200 OK"` to indicate a successful request.  
- The **Content-Length** header is included to specify the size of the HTML content being sent.  
- Finally, the actual **HTML content** is appended as the response **body**.  

Once the response is fully prepared, it is written to the **TCP stream** using the `write_all` method, ensuring that the browser receives and renders the HTML correctly.  
