# Research topics
## HTTP vs HTTPS
### Difference between HTTP & HTTPS
- HTTP : stands for Hyper Text Transfer Protocol is an application protocol which allow users to communicate data on the world wide web .
- HTTPS :stands for hypertext transfer protocol secure and is the encrypted version of HTTP. 
- The main difference between them is in HTTP: No Data Encryption Implemented and the data send as plain text but in HTTPS: Encrypted Connections it uses SSL (Secure Sockets Layer), which encrypts the request and response.
- These are the general deferences between HTTP & HTTPS :
    - In HTTP, URL begins with “http://” whereas URL starts with “https://”
    - HTTP uses port number 80 for communication and HTTPS uses 443
    - HTTP is considered to be unsecure and HTTPS is secure
    - HTTP Works at Application Layer and HTTPS works at Transport Layer
    - HTTP does not require any certificates and HTTPS needs SSL Certificates
### How does HTTPS work? What are TLS/SSL certificates?
HTTPs encrypts the data unlike HTTP which sends the data as plaintext.HTTPS secures the connection using SSL cirtificate.
- What is SSl ?
SSl is an abbreviation for "secure sockets layer" it  protects the layer of communication between the client and the server by creating a secure, encrypted connection between them.And it make sure that any data transferred between client and server, remain impossible to read. It do this by using  encryption algorithms.
- What is TLS ?
 TLS stands for transport layer security and is just an updated, more secure, version of SSL.
TLS  using a tichnique known as  TLS handshake ,this ensures three things :
    - ensure data has not been tampered with since it was sent and this means ensures integrity of data.
    - ensures that communications are with the actual person the communication came from and this means ensures authentication.
    - prevent private data from being seen and this\ done by encryption.
    
### Why is this important to implement in your projects?
HTTPS  is important in projects because it protects all communication and customer information. HTTPS also works to legitimize any site that uses it because businesses that use HTTPS can be verified. In the case of any e-commerce site, in particular, customers will feel safer shopping there.

### Demo how to generate certificates and use them in a node project
Using HTTPS module 
```js
// use https module
const https = require("https");
// use fs module
  fs = require("fs");

const options = {
  key: fs.readFileSync("/srv/www/keys/my-site-key.pem"), // the private key
  cert: fs.readFileSync("/srv/www/keys/chain.pem") // the certificate
};

const app = express(); // use express

app.use((req, res) => {
  res.writeHead(200);
  res.end("hello world\n");
});

app.listen(8000);

https.createServer(options, app).listen(8080); // create server using HTTPS and including the private key and certificate
```


 
