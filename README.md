
Using “urllib” library to fetch web objects a
nd perform Wireshark analysis




Introduction: “Urllib” is a Python standard library recommended for HTTP tasks. The standard library also has a low-level module called http. Although this offers access to almost all aspects of the protocol, it has not been designed for everyday use. For making requests and receiving responses, we employ the urllib.request module. Retrieving the contents of a URL is a straightforward process when done using urllib.
Objectives: To use urllib package to extract the details such as headers and content in requests and responses under HTTP. To appreciate the advantage over socket package when dealing with HTTP. To compare and verify the results with Wireshark.
Request with urllib:
The urllib package is broken into several submodules for dealing with the different tasks that we may need to perform when working with HTTP. For making request and receiving responses, we employ the urllib.request module.


          
We are sending a request and receiving a response from ' http://gaia.cs.umass.edu/wiresharklabs/alice.txt.org’using urlopen in the above example. Response.url prints the URL accessed . Readline reads the first line of the Html response

The response.readlines() reads the content line-by-line and response.read(50) reads the first 50 bytes of the Html response.
Status Code:
Status codes are integers that tell how the request went, different codes convey different meanings.
The status code 200 indicates the request was successful.
Handling HTTP and URL Errors
Status codes help us to see whether our response was successful or not. Any code in the 200 range indicates a success, whereas any code in either the 400 range or the 500 range indicates failure.  Status codes should always be checked so that our program can respond appropriately if something goes wrong. The urllib package helps us in checking the status codes by raising an exception if it encounters a problem.


 
The code attempts to open a URL by using urlopen('http://www.ietf.org/rfc/rfc0.txt'), which targets the specified web address. If accessing the URL leads to an HTTP error, such as a 404 Not Found, 403 Forbidden, or 500 Internal Server Error, the program triggers an HTTPError exception. In the event of an HTTPError, the code catches the exception and displays relevant error information, including the HTTP status code (e.g., 404), the reason phrase corresponding to that code (e.g., "Not Found"), and the URL that caused the error.

In this instance, we have asked for index.html from the 192.0.2.1. host. The 192.0.2.0/24 IP address range is reserved to be used by documentation only, so you will never encounter a host using the preceding IP address. Hence the TCP connection times out and socket raises a timeout exception, which urllib catches, re-wraps, and re-raises for us. HTTPError occurs when the request reaches the server, but the server returnsan error (e.g., 404 Not Found). URLError occurs if the request cannot connect to the server (e.g., connection timeout).
HTTP headers: 
Headers are the lines of protocol-specific information that appear at the beginning of the raw message that is sent over the TCP connection. The getheaders() method returns a list of response headers, which contain metadata such as server information and content type. It displays a list of headers as (name, value) pairs.









Customizing Requests with Headers:

The above code adds the Accept-Language header to request content in Swedish. If the server supports it, it returns the content in the requested language. It displays the first 5 lines of content in Swedish.

The above code is used to view the headers present in the request and creates a Request object for the Debian homepage, adding headers directly during initialization. Headers are supplied as a dictionary to the Request object constructor as the headers keyword argument. In this way we can add multiple headers in one go, by adding more entries to the dictionary.
 Content Compression:
The Accept-Encoding request header and the Content-Encoding response header work together to temporarily encode the body of a response for efficient transmission over the network, primarily for compression purposes. The process begins when the client sends a request that lists acceptable encodings in the Accept-Encoding header. The server then selects a supported encoding method and applies it to the response body. Subsequently, the server sends the response back to the client, indicating the chosen encoding method in the Content-Encoding header. Finally, the client decodes the response body using the specified encoding method, enabling reduced data transfer and improved performance.



Decompressing Gzip


The Accept-Encoding header requests gzip-compressed content. The response is decoded using the gzip module to access readable content. Displays the content-encoding type and the first few lines of decompressed content.






Multiple Values 
To tell the serve that we can accept more than one encoding, add more values to the Accept-Encoding header and separate them by commas.

Multiple encoding Preferences 
Multiple encodings are specified, with q values indicating preference.gzip is preferred, followed by deflate with lower priority, and identity with the lowest.



Above image shows Reading Content-Type and Charset 




The Content-Type header informs the client of the content type (e.g.,text/html). The charset parameter provides the encoding (UTF-8 in this case), which is used to decode the content.





User Agents 
Any client that communicates using HTTP can be referred to as a user agent. RFC 7231 suggests that user agents should use the User-Agent header to identify themselves in every request.






Webmasters often inspect the user agents of requests to gather insights for various purposes, such as classifying website visits for statistical analysis, blocking clients with specific user agent strings, and sending alternative versions of resources to user agents known to have issues—like bugs in CSS interpretation or lack of support for languages like JavaScript. However, these practices can hinder access to desired content. To circumvent such restrictions, users can modify their user agent to mimic that of a well-known browser, a technique referred to as spoofing.





Conclusion: The python codes have been executed and the HTTP packets have been captured. In conclusion, using the urllib package to handle HTTP requests and responses provides a more efficient and user-friendly approach compared to the socket package.


