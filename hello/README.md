## Commit 1 Reflection
BufReader, wraps the TcpStream and provides buffered reading.  Instead of reading one byte at a time directly from the stream, it reads chunks of data into a buffer, making it more efficient to read line by line.
.lines(), returns an iterator over the lines of the stream. Each item in the iterator is a Result<String>, so we use .map(|result|result.unwrap()) to extract the actual String value from each line.
.take_while(|line| !line.is_empty()) stops at an empty line because in HTTP the headers are separated from the body by a blank line so .take_while(|line| !line.is_empty()) keeps reading lines until it hits that empty line, which means we only collect HTTP request headers and nothing else.
final Vec contains all the HTTP request header lines as String:
"GET / HTTP/1.1",
"Host: 127.0.0.1:7878",
"Connection: keep-alive",

## Commit 2 Reflection
fs::read_to_string, is used to more conveniently read entire contents of a file into a single string. The server then contructs a proper HTTP response with status line 'HTTP/1.1 200 ok', 'Content-Length' header to know how many bytes expected, blank line ('\r\n\r\n') to seperate header from body, and HTML content
Content-Length, is a HTTP header used to indicate the size of the request or response body in bytes.
when opening http://127.0.0.1:7878, the browser successfully rendered the HTML page with
Hello!
Hi from Rust, running from khay's machine
hence confirming that the server now reads the HTML file and serve it as a proper HTML response.
![Commit 2 screen capture](milestone2.png)