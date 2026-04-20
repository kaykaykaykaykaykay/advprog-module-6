## Commit 1 Reflection
BufReader, wraps the TcpStream and provides buffered reading.  Instead of reading one byte at a time directly from the stream, it reads chunks of data into a buffer, making it more efficient to read line by line.
.lines(), returns an iterator over the lines of the stream. Each item in the iterator is a Result<String>, so we use .map(|result|result.unwrap()) to extract the actual String value from each line.
.take_while(|line| !line.is_empty()) stops at an empty line because in HTTP the headers are separated from the body by a blank line so .take_while(|line| !line.is_empty()) keeps reading lines until it hits that empty line, which means we only collect HTTP request headers and nothing else.
final Vec contains all the HTTP request header lines as String:
"GET / HTTP/1.1",
"Host: 127.0.0.1:7878",
"Connection: keep-alive",