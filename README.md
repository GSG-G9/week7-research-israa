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


## Stateless vs stateful authentication
### What is session based authentication (stateful) vs token based authentication (stateless)?
  - session based authentication (stateful) : , the server will create a session for the user after the user logs in. The session id is then stored on a cookie on the user’s browser. While the user stays logged in, the cookie would be sent along with every subsequent request. The server can then compare the session id stored on the cookie against the session information stored in the database to verify user’s identity and sends response with the corresponding state.

- token based application, the server creates JWT with a secret and sends the JWT to the client. The client stores the JWT  in browser and includes JWT in the header with every request. The server would then validate the JWT with every request from the client and sends response.

- The main difference between session and token based autentication is that in session the session stored in the database while in the token the user state stored in the browser.

### Draw flow diagrams to show the steps involved in each process
session based authentication diagram 

![Stateful session diagrams](https://miro.medium.com/max/3000/1*Hg1gUTXN5E3Nrku0jWCRow.png)

token based authentication diagram 

![Stateless token diagrams](https://miro.medium.com/max/3000/1*PDry-Wb8JRquwnikIbJOJQ.png)


### What are the advantages and disadvantages of each?
Stateless session :
   - advantages:
      - Reduces memory usage
      - Reduces session expiration issue

   - disadvantages:
      - Harder to maintain user interaction and create a seamless web application.
      - May require extra information to be sent to and from a client.
Statefull session :
   - advantages:
      - Keep track of a user throughout a web application/site
      - More intuitive - Entity data can be maintained on the server between requests.
      - Can sometimes improve performance when retrieval of data is only required once.

   - disadvantages:
      - Requires memory to be allocated to store the data.
      - Can lead to a performance decrease if session storage is not maintained efficiently.


## Session-management in Express
### What are sessions?
A session can be defined as a server-side storage of information that is desired to persist throughout the user's interaction with the web site or web application. 

Instead of storing large and constantly changing information via cookies in the user's browser, only a unique identifier is stored on the client side (called a "session id"). This session id is passed to the web server every time the browser makes an HTTP request . The web application pairs this session id with it's internal database and retrieves the stored variables for use by the requested page.

### What are the different ways of managing sessions in express?
  - use express session 
```js
const express = require('express');
const session = require('express-session');
const app = express();
```
then 

```js
app.use(session({secret: 'ssshhhhh'}));
```
full example here :
https://codeforgeek.com/manage-session-using-node-js-express-4/

In nodejs 
- client session : client-sessions is connect middleware that implements sessions in encrypted tamper-free cookies.
for more details refer to the documentation here https://www.npmjs.com/package/cookie-session

 
### Create a minimal example of how to set up a session (FYI: pseudo code is fine)
```js
- install express-session --> npm install express-session
- in server.js file do the following :
const express = require('express');
const session = require('express-session');
const app = express();
- After this, we have to initialize the session and we can do this by using following
app.use(session({secret: 'ssshhhhh'})); // Here ‘secret‘ is used for cookie handling
-  using ‘request‘ variable you can assign session to any variable.

```

## Attacks

### Man In The Middle (MITM)
is a cyberattack where the attacker secretly relays and possibly alters the communications between two parties who believe that they are directly communicating with each other.
The goal of an attack is to steal personal information, such as login credentials, account details and credit card numbers.

![Man In The Middle Attack](https://phoenixnap.com/blog/wp-content/uploads/2019/03/how-man-in-middle-works-min.png)

Types of attack :
- IP spoofing
- Email hijacking
- HTTPS spoofing
- Wi-Fi eavesdropping

#### How to prevent man-in-the-middle attacks?
 - don’t use public networks.
 - Secure your e-mails by employing SSL/TLS.
 - Using a VPN : a VPN (virtual private network) encrypt the data as it’s being transmitted over the Internet. This doesn’t make you impenetrable to MITM attacks, but it makes life much harder for crooks.
 - Only visiting HTTPS websites : As with VPNs, HTTPS websites encrypt data and prevent attackers from intercepting communications.
- Watching out for phishing scams
![Prevent Man In The Middle Attack](https://dpsvdv74uwwos.cloudfront.net/statics/img/ogimage/man-in-the-middle-attack-how-avoid.png)


 ### Cross Site Scripting (XSS)
Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser side script
![ Cross Site Scripting ](https://avinetworks.com/wp-content/uploads/2020/09/cross-site-scripting-diagram.png)
#### How to prevent XSS attacks
 - Filter input on arrival. At the point where user input is received, filter as strictly as possible based on what is expected or valid input.
 - Encode data on output. At the point where user-controllable data is output in HTTP responses, encode the output to prevent it from being interpreted as active content. Depending on the output context, this might require applying combinations of HTML, URL, JavaScript, and CSS encoding.
 - Use appropriate response headers. To prevent XSS in HTTP responses that aren't intended to contain any HTML or JavaScript, you can use the Content-Type and X-Content-Type-Options headers to ensure that browsers interpret the responses in the way you intend.
 - Content Security Policy. As a last line of defense, you can use Content Security Policy (CSP) to reduce the severity of any XSS vulnerabilities that still occur.
 
