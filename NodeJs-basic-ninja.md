# Lesson 1: Introducting to Nodejs
- NodeJS: It's allow you coding Javascript direct without run browser.
- V8: is Google’s open source high-performance JavaScript and WebAssembly engine, written in C++. It is used in Chrome and in Node.js, among others. It implements ECMAScript and WebAssembly, and runs on Windows, macOS, and Linux systems that use x64, IA-32, or ARM processors. V8 can be embedded into any C++ applicatio

- Relationship between V8 and Nodejs:
V8 is the Javascript engine inside of node. js that parses and runs your Javascript.
# Lesson2: NodeJs basic

## 1. Global object: These objects are available in all modules.
- __dirname  : return current folder path 
- __filename  : return current file path 
- exports  : exports 
- module
- require()

# Lesson 3: Clients & Servers

## 1. IP Address: 
A computer will have its own ip address. It is a sequence of numbers for example:
216.58.216.164

It is hard view for users to access the computer with the above address range being difficult to remember. Therefore, domains were born to hide IP addresses that are easy to see and read

## 2. Localhost:
It is ip address 127.0.0.1, localhost means your computer is communicating with itself. Helps you develop client server application websites without needing to connect to another IP address

## 3. Port: 
Software A that wants to communicate with a software B (where B is the server) needs two things:
1 is the host (ip address) of the server containing software B.

2 is a port of software B,When B opens the port, A only needs to follow the correct port and correct IP Address of B to get resources

    Ex:
    localhost:3000
    That mean:
    127.0.0.1:3000
    
# Lesson 4: Requests & Responses

## 1. Requests
When you create a server by Nodejs, client who want to use your server will send 1 request to server on port and IP Address ( or your domain server).
The request can be basic include:
- Header [Header MDN details..](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- body 
- Url 
- params, domain, query,...
- ... another

## 2. Response
As you know, client sending a request to server then sever will return data to client. Response to do this. You can see bellow:
### Ex1: Server response a html code to client
```js
const fs = require('fs') // to import IO file.
const server = http.createServer((req, res) => {
    res.setHeader('Content-type', 'text/html')
    //To read file you must create folder view and index file
    fs.readFile('./view/index.html', (err, data)=>{
        if(err){
            console.log("🚀 ~ fs.readFile ~ err:", err)
            res.end()
        }
        res.write(data)
        res.end()
    })
})
```
### Ex2: Server response a JSON data to client
```js
const server = http.createServer((req, res) => {
    res.setHeader('Content-type','application/json')
    const data = {
        name:"developer",
        role :"admin"
    }
    // this is expressJs code
    res.json(data)
})
```
### Ex3: Server response a Object to client
```js
const server = http.createServer((req, res) => {
    res.setHeader('Content-type', 'text/plain')
    res.write('Hello world!!')
    res.end()
})
```

## 3. Basic Routing (ExpressJs)
Routing refers to determining how an application responds to a client request to a particular endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, and so on).

```js
app.METHOD(PATH, HANDLER)
```
Where:
- app is an instance of express.
- METHOD is an HTTP request method (get,post, put )
- PATH is a path on the server. (domain, url, localhost,IP address,... )
- HANDLER is the function executed when the `route is matched.`

###  Example two method usually use :
Get method
```js
app.get('/', (req, res) => {
  res.send('Hello World!')
})
```
Post method
```js
app.post('/', (req, res) => {
  res.send('Got a POST request')
})
```
## 4. Status code

HTTP response status codes indicate whether a specific HTTP request has been successfully completed. Responses are grouped in five classes:

- Informational responses (100 – 199)
- Successful responses (200 – 299)
- Redirection messages (300 – 399)
- Client error responses (400 – 499)
- Server error responses (500 – 599)

You can see detail status here: [wikipedia_status_code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

### Example response status code by ExpressJs
```js
//res.status(code)
res.status(403).end()
res.status(400).send('Bad Request')
res.status(404).sendFile('/absolute/path/to/404.png')
```

# Lesson 5. Express Apps
ExpressJs is a framework that makes it easy to write logical nodejs code and build fast server side.
## 1. How to use ?
To use express you can install by `npm i express` , then you can use express:
```js
const express  = require('express') // this is a function
const app  = express() // we create 1 app express
    app.listen(3000, ":::App listen on port 3000....")
    //this app running and app's port is 3000
```
## 2. Implement router
Use can create router by express:
```js
app.get('/',(req, res)=>{
        res.send("Hello world")
})
```
## 3. How to send file to Client ?
Express have function `sendFile` it's syntax and paramaters is:
#### Syntax:
```
res.sendFile('path_file_to_send', { root:<current_folder_project>} )
```

#### Paramaters
- `path_file_to_send`: your path file will send
- `<current_folder_project>` : your folder path(or your  project path )

### Example:
```js
app.get('/',(req, res)=>{
        res.sendFile("./view/index.html", {root: __dirname}) 
        //__dirname: get current path folder
})
```