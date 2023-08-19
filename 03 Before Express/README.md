> PARADIGM: "Open Book Exam" aka Reference module-docs mentality

<br>

#### 5. [Pre-Express](#5)

#### 6. [How the Internet Works - TCP and UDP](#6)

#### 7. [What is an HTTP request and how does it work?](#7)

#### 8. [Course Housekeeping - How I do Nodejs](#8)

#### 9. [Node/HTTP servers 101](#9)

#### 10.[ Serving up routes and static files in plain Node (no fun...)](#10)

#### 11.[ Serving up routes and static files... continuted](#11)

#### 12.[ What is Networking from dev perspective](#12)

<br>

### 5. Pre-Express<a id='5'></a>

- Network(server & client) protocol: http, tcp, udp, ftp, smtp, ssh

<br>

### 6. How the Internet Works - TCP and UDP<a id='6'></a>

- How packet are sent over, dev perspective

<img src="notes/1%20data%20transfer%20in%20packet.png" width="500">

<br>

- Network (client & server) protocol

<img src="notes/2%20developer%20perspective.png" width="500">

<br>

- Feature of UDP
- vdieo chat, online games, live communication

<img src="notes/4%20UDP%20feature.png" width="500">

<br>

- Feature of TCP

<img src="notes/5%20TCP%20feature.png" width="500">

<br>

- TCP vs UDP

<img src="notes/6%20TCP%20vs%20UDP.png" width="500">

<br>

### 7. What is an HTTP request and how does it work?<a id='7'></a>

- Http can send following stuff, in-forms of packets to other browser from server

<img src="notes/8%20http%20can%20send%20following%20.png" width="500">

<br>

- How do http msg look like

```sh
 http message layout
 1. start-line
 2. header
 3. body
```

<img src="notes/9%20how%20do%20http%20msg%20look%20like.png" width="500">

<br>

- How to do curl in Vs code Terminal "cmd prompt"

```sh
   curl -v www.google.com
```

<img src="notes/11%20curl%20request.png" width="500"><br>
<img src="notes/15%20format%20of%20start%20line.jpg">

- Http message start line, request send from curl-client/browser to google server
  <img src="notes/12%20http%20msg%20start%20line.png" width="500">

<br>

- Http message headers received from google server
  <img src="notes/13%20http%20msg%20headers.png" width="500">

<br>

- Http body received from google server: Here is the text or binary stuff
  <img src="notes/14%20http%20msg%20body.png" width="500">

<br>

### 8. Course Housekeeping - How I do Nodejs<a id='8'></a>

- [nodemon](https://www.npmjs.com/package/nodemon)

```sh
npm install -g nodemon
```

<br>

### 9. Node/HTTP servers 101<a id='9'></a>

- How to run nodeServer?
- navigate to http module and run

```sh
nodemon nodeServer
```

---

- req object: this is what we know about the requesting machine, where http request comes in

- How to create native http server using [http module](https://www.w3schools.com/nodejs/nodejs_http.asp "mdn")

<br>

### 10. Serving up routes and static files in plain Node (no fun...)<a id='10'></a>

- What are the most common [mime type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types "mdn") use in http headers

<br>

### 11. Serving up routes and static files... continuted<a id='11'></a>

<br>

### 12. What is Networking from dev perspective<a id='12'></a>
