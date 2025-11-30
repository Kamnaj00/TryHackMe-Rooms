# HTTP(S) in Detail

---

## Task 1 – What is HTTP(S)?

###  Definition
- **HTTP (HyperText Transfer Protocol):**  
  Protocol for requesting and transmitting web content (HTML, images, videos).  
  Developed by Tim Berners‑Lee (1989–1991).  

- **HTTPS (HyperText Transfer Protocol Secure):**  
  Encrypted version of HTTP using TLS/SSL.  
  Ensures:
  - **Confidentiality**: Data is encrypted.  
  - **Integrity**: Data cannot be modified unnoticed.  
  - **Authentication**: Confirms you’re talking to the correct server.  

### Q&A

- Q: What does HTTP stand for?
- A: HyperText Transfer Protocol ✅
- Q: What does the S in HTTPS stand for?
- A: Secure ✅
- Q: Challenge flag
- A: THM{INVALID_HTTP_CERT} ✅


### Diagram – HTTP vs HTTPS
```mermaid
flowchart TD
    Browser[Client Browser] -->|HTTP - unencrypted| Server[Web Server]
    Browser -->|HTTPS - TLS/SSL encrypted| SecureServer[Secure Web Server]
```
## Task 2 – Requests and Responses

### URL Structure

| Component    | Description                  | Example            |
|--------------|------------------------------|--------------------|
| Scheme       | Protocol used                | `https://`         |
| User         | Optional login credentials   | `user:pass@`       |
| Host         | Domain name or IP address    | `tryhackme.com`    |
| Port         | Connection port              | `:443`             |
| Path         | Resource location            | `/blog`            |
| Query String | Parameters                   | `?id=1`            |
| Fragment     | Page anchor                  | `#section`         |


### Diagram – URL Breakdown

```mermaid
flowchart LR
    Scheme[Scheme: https] --> User[User: user:pass@]
    User --> Host[Host: tryhackme.com]
    Host --> Port[Port: 443]
    Port --> Path[Path: /blog]
    Path --> Query[Query: ?id=1]
    Query --> Fragment[Fragment: #section]
```
### Example URL

https://user:pass@tryhackme.com:443/blog?id=1#section

### Explanation:

- Scheme: https:// → Use HTTPS protocol.

- User: user:pass@ → Optional credentials.

- Host: tryhackme.com → Domain name.

- Port: :443 → HTTPS default port.

- Path: /blog → Resource location.

- Query String: ?id=1 → Parameter for resource.

- Fragment: #section → Anchor to part of the page.

### Example Request
```http
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

### Example Response
```http
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98
```
```html
<html>
<head><title>TryHackMe</title></head>
<body>Welcome To TryHackMe.com</body>
</html>
```

### Diagram – Request/Response Flow
```mermaid
sequenceDiagram
    participant Browser as Browser
    participant Server as Web Server

    Browser->>Server: HTTP Request (GET /index.html)
    Server-->>Browser: HTTP Response (200 OK + HTML)
  ```

### Q&A

- Q: What HTTP protocol is being used in the above example?
- A: HTTP/1.1 ✅
- Q: What response header tells the browser how much data to expect?
- A: Content-Length ✅

## Task 3 – HTTP Methods

### Definition
HTTP methods define the **intended action** of the client when making a request to a server.  
They tell the server *what you want to do* with the resource.

### Common Methods

| Method  | Purpose                          | Example Request                |
|---------|----------------------------------|--------------------------------|
| GET     | Retrieve data                    | `GET /news.html`               |
| POST    | Submit data / create new records | `POST /register`               |
| PUT     | Update existing data             | `PUT /user/2`                  |
| DELETE  | Remove data                      | `DELETE /user/1`               |


### Diagram – Methods in Action

```mermaid
flowchart TD
    Client[Client Browser] -->|GET| Server[Web Server]
    Client -->|POST| Server
    Client -->|PUT| Server
    Client -->|DELETE| Server
```
### Q&A
- Q: What method would be used to create a new user account?
- A: POST ✅
 
- Q: What method would be used to update your email address?
- A: PUT ✅
 
- Q: What method would be used to remove a picture you've uploaded to your account?
- A: DELETE ✅
 
- Q: What method would be used to view a news article?
- A: GET ✅

## Task 4 – HTTP Status Codes

### Definition
When a web server responds to a request, the **first line** of the response contains a **status code**.  
This code tells the client the **outcome of the request** and how to handle it.

### Status Code Ranges

| Range   | Category            | Meaning                                                                 |
|---------|---------------------|-------------------------------------------------------------------------|
| 100–199 | Informational       | Request received, continue process. Rarely used today.                  |
| 200–299 | Success             | Request was successful.                                                 |
| 300–399 | Redirection         | Client must take additional action (redirect to another resource).      |
| 400–499 | Client Errors       | Error caused by the client request (missing data, unauthorized, etc.).  |
| 500–599 | Server Errors       | Error caused by the server (crash, overload, misconfiguration).          |

### Common Status Codes

| Code | Meaning               | Example Use Case                                      |
|------|-----------------------|-------------------------------------------------------|
| 200  | OK                    | Request completed successfully.                       |
| 201  | Created               | New resource created (user account, blog post).       |
| 301  | Moved Permanently     | Resource moved to a new URL.                          |
| 302  | Found (Temporary)     | Resource temporarily redirected.                      |
| 400  | Bad Request           | Client sent invalid or incomplete request.            |
| 401  | Not Authorized        | Authentication required (e.g., login needed).         |
| 403  | Forbidden             | Client does not have permission to access resource.   |
| 404  | Page Not Found        | Requested resource does not exist.                    |
| 405  | Method Not Allowed    | Wrong HTTP method used (e.g., GET instead of POST).   |
| 500  | Internal Server Error | Server crashed or encountered unexpected condition.   |
| 503  | Service Unavailable   | Server overloaded or down for maintenance.            |

### Diagram – Status Code Flow

```mermaid
flowchart TD
    Request[Client Request] --> Server[Web Server]
    Server --> Success[200–299 Success]
    Server --> Redirect[300–399 Redirection]
    Server --> ClientError[400–499 Client Error]
    Server --> ServerError[500–599 Server Error]
```

### Example Response with Status Code
```http
HTTP/1.1 404 Not Found
Date: Sun, 30 Nov 2025 13:14:00 GMT
Server: nginx/1.15.8
Content-Type: text/html
Content-Length: 120
```

```html
<html>
<head><title>404 Not Found</title></head>
<body>Sorry, the page you requested does not exist.</body>
</html>
```
### Q&A
- Q: What response code might you receive if you've created a new user or blog post article?	2
- A: 01 Created ✅
- Q: What response code might you receive if you've tried to access a page that doesn't exist?
- A: 404 Not Found ✅
- Q: What response code might you receive if the web server cannot access its database and the application crashes?
- A: 500 Internal Server Error ✅
- Q: What response code might you receive if you try to edit your profile without logging in first?
- A: 401 Not Authorized ✅

## Task 5 – Headers

### Definition
Headers are **additional bits of data** sent between client and server during HTTP communication.  
They provide **metadata** about the request or response, such as browser type, content length, or caching rules.


### Common Request Headers

| Header         | Description                                                                 | Example                                |
|----------------|-----------------------------------------------------------------------------|----------------------------------------|
| Host           | Specifies which website/domain is being requested                           | `Host: tryhackme.com`                  |
| User-Agent     | Identifies browser software and version                                     | `User-Agent: Mozilla/5.0 Firefox/87.0` |
| Content-Length | Size of data being sent in the request                                      | `Content-Length: 98`                   |
| Accept-Encoding| Compression methods supported by the client                                | `Accept-Encoding: gzip, deflate`       |
| Cookie         | Sends stored cookie data to the server                                     | `Cookie: sessionid=12345`              |


### Common Response Headers

| Header         | Description                                                                 | Example                                |
|----------------|-----------------------------------------------------------------------------|----------------------------------------|
| Set-Cookie     | Saves cookie on client for future requests                                  | `Set-Cookie: sessionid=12345`          |
| Cache-Control  | Defines caching rules for the browser                                       | `Cache-Control: max-age=3600`          |
| Content-Type   | Specifies type of returned data (HTML, CSS, JSON, images, etc.)             | `Content-Type: text/html`              |
| Content-Encoding| Compression method used by the server                                     | `Content-Encoding: gzip`               |


### Diagram – Header Exchange

```mermaid
sequenceDiagram
    participant Browser as Client Browser
    participant Server as Web Server

    Browser->>Server: Request Headers (Host, User-Agent, Cookie, etc.)
    Server-->>Browser: Response Headers (Content-Type, Set-Cookie, Cache-Control, etc.)
```
### Example Request with Headers
```http
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Accept-Encoding: gzip, deflate
Cookie: sessionid=12345
```
### Example Response with Headers
```http
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Sun, 30 Nov 2025 13:25:00 GMT
Content-Type: text/html
Content-Length: 120
Set-Cookie: sessionid=12345
Cache-Control: max-age=3600
Content-Encoding: gzip
```
### Q&A

- Q: What header tells the web server what browser is being used?
- A: User-Agent ✅
- Q: What header tells the browser what type of data is being returned?
- A: Content-Type ✅
- Q: What header tells the web server which website is being requested?
- A: Host ✅

## Task 6 – Cookies

### Definition
- **Cookies** are small pieces of data stored on your computer by a web server.  
- They are saved when the server sends a **`Set-Cookie`** header in its response.  
- On every subsequent request, your browser sends the cookie back using the **`Cookie`** header.  
- Because HTTP is **stateless** (does not remember previous requests), cookies are used to:
  - Identify users (authentication).  
  - Store personal settings.  
  - Track whether you’ve visited a site before.  


### Example – Cookie Exchange

### Response from Server
```http
HTTP/1.1 200 OK
Content-Type: text/html
Set-Cookie: sessionid=abc123; Path=/; HttpOnly
Subsequent Request from Browser
```
```http
GET /dashboard HTTP/1.1
Host: example.com
Cookie: sessionid=abc123
```
### Diagram – Cookie Lifecycle
```mermaid
sequenceDiagram
    participant Browser as Client Browser
    participant Server as Web Server

    Server-->>Browser: Response Header (Set-Cookie: sessionid=abc123)
    Browser->>Server: Request Header (Cookie: sessionid=abc123)
```
### Viewing Cookies
- Use Developer Tools in your browser.

- Open the Network tab → select a request → check the Cookies tab.

- You’ll see cookies sent by your browser and those set by the server.

### Q&A
- Q: Which header is used to save cookies to your computer?
- A: Set-Cookie  ✅

## Task 7 – Making Requests

### Definition
HTTP requests are instructions sent from the client (browser) to the server.  
They specify the **method** (GET, POST, PUT, DELETE), the **endpoint** (path), and optionally **parameters** or **body data**.

### Example Requests

#### ✅ GET Request – `/room`
```http
GET /room HTTP/1.1
Host: example.com
```
#### ✅ GET Request – /blog?id=1

```http
GET /blog?id=1 HTTP/1.1
Host: example.com
```
#### ✅ DELETE Request – /user/1

```http
DELETE /user/1 HTTP/1.1
Host: example.com
```
#### ✅ PUT Request – /user/2 with body parameter

```http
PUT /user/2 HTTP/1.1
Host: example.com
Content-Type: application/json
Content-Length: 32
{"username":"admin"}
```

#### ✅ POST Request – /login with body parameters

```http
POST /login HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 32
username=thm&password=letmein
```

### Diagram – Request Flow
```mermaid
sequenceDiagram
    participant Browser as Client Browser
    participant Server as Web Server

    Browser->>Server: GET /room
    Server-->>Browser: Response (200 OK)

    Browser->>Server: GET /blog?id=1
    Server-->>Browser: Response (200 OK + Blog Article)

    Browser->>Server: DELETE /user/1
    Server-->>Browser: Response (200 OK + User Deleted)

    Browser->>Server: PUT /user/2 {username: admin}
    Server-->>Browser: Response (200 OK + User Updated)

    Browser->>Server: POST /login {username: thm, password: letmein}
    Server-->>Browser: Response (200 OK + Auth Token)
```
### Q&A

- Q: Make a GET request to /room page	GET /room
- A: THM{YOU'RE_IN_THE_ROOM} ✅

- Q :Make a GET request to /blog page with id=1	GET /blog?id=1
- A: THM{YOU_FOUND_THE_BLOG} ✅
 
- Q: Make a DELETE request to /user/1 page	DELETE /user/1
- A: THM{USER_IS_DELETED} ✅
  
- Q: Make a PUT request to /user/2 with username=admin	PUT /user/2 {username: admin}
- A: THM{USER_HAS_UPDATED} ✅
  
- Q: Make a POST request to /login with username=thm and password=letmein	POST /login {username=thm, password=letmein}
- A: THM{HTTP_REQUEST_MASTER} ✅

