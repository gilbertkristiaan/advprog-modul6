# Gilbert Kristian - Adpro A - 2306274951

# Milestone 1: Single-Threaded Web Server  

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


