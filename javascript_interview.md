
ES-2026 Latest features
-------------------------------------

In recent es-2026 there are several features has introduced, those are listed below

Array.fromAsync()
Iterator.concat()
Math.preciseSum()
Error.isError()
Object.groupBy()
Map.groupBy()
toSorted()
toReversed()
toSliced()

Array.fromAsync():- 
This creates an array from async iterable.

Example: 
async function* getUsers(){

	yield "one";
	yield "two";
	yield "three";	
}

const users = await Array.fromAsync(getUsers());

console.log(users);
// ['John', 'Peter', 'David']

Iterator.concat()

It allows multiple iterators to be combined into one sequentially.

Example: 

var recordOne = [1,2,3];
var recordTwo = [4,5,6];

var combinedResult = Iterator.concat(recordOne, recordTwo);
console.log([...combinedResult])




first class function
--------------------

first class function is a function which will act like an variable that can be stored and then used

var handler = ()=> console.log("this is a first class function!!!");

document.addEventListener("click", handler);

firstOrder function
-------------------

first order function is a function which will not take any other function as an argument and does not return a function as return value

const firstOrder = ()=> console.log("This is a first order function!!!");

Higher order function
---------------------
A higher order function is a function that either accepts a function as an argument or it can return a value 



	Nodejs
========================

Q) What is error first callback ?

Error first callback is use to pass errors and data. The first argument of the callback is always error object that the programmer has to check something went wrong.
Other additional arguments are used to pass data.


Example_1:

	function callback(error, result){
		if(error) {
		  throw new Error("Some error occurred!!!")
		}
	console.log(data);
		return result;
	}


Example_2:

	const fs = require('fs');

	
	fs.readFile('userdetails.txt', 'utf-8', (error, data)=>{
		if(error){
			throw new Error("Unable to read file");
			console.log("Something went wrong", error);
			return;	
		}
	return data
		
});


Q) What's the difference between operational and programmer errors? 

Operational errors: These are not actual bugs, these errors are occurs when there is a system failure or request timeout, hardware failure.
Programmer errors: There are actual bugs and all related to the code failure.


Q) What is difference between API and REST API?

API(Application Programming Interface)
Definition: API is an interface that allows to communicate in between two applications each other.

REST API
Definition: REST API is an API that follows the REST principle and uses HTTP methods like GET, POST, PUT, PATCH and DELETE to work with resources.

NOTE: Every REST API is an API, but not every API is a REST API.
      REST stands for (Representational State Transfer)



Q) List out all the methods of REST API ?

There are several REST API methods available GET, POST,PUT, PATCH, DELETE

GET: Used to GET/Read the data. e.g. GET /api/users
POST: Used to create new data. e.g. POST /api/users
PUT: Used to update/replace existing data. e.g. PUT api/users/90
PATCH: Used to update part of the data e.g. PATCH api/users/90
DELETE: delete data. e.g. api/users/90


Realtime examples:

const express = require("express");

const app = express();

app.use(express.json());

app.get("/users", (req, res)=>{
	res.send("Get Users!!!");
});


app.post("/users/:id", (req, res)=>{
	res.send(`Create user`);
});

app.put("/users/:id", (req, res)=>{
	res.send(`Replace User${req.params.id}`);
});

app.patch("/users/:id", (req, res)=>{
	res.send(`Update part of the user data ${req.params.id}`)
});


app.delete("/users/:id", (req, res)=>{
	res.send(`Delete one user${req.params.id}`);
});


app.listen(3000. ()=>{
	console.log("Server is running in 3000")
});



Q12: If Node.js is single threaded then how it handles concurrency?

Node.js uses a single JavaScript  thread with an event loop and non-blocking I/O. Time consuming I/O
operations are handled outside the JavaScript thread, allowing Node.js to continue processing other requests instead of waiting.

Q13 What is Callback Hell? 

In nodejs javascript asunchronous functions need a callback function to return as a parameter, When multuiple asynchronous functions are chained together then callback hell situation comes up.
In this case its very difficult to read, write, debug and maintain the code.

Note: We can handle callback hell using Promise, async/await


Example: 


	The Problem:
	
	function getUser((user)=>{
		getOrder((order)=>{
			getOrderDetails((orderdetails)=>{
				console.log(orderdetails)
			});
		});
	});

	The Solution:

	getUser().then((user)=>{
		getOrder(user.id)	
	}).then((orders)=>{
	
		getOrderDetails((details)=>{
			console.log(details)
		})
	}).catch(err=>{
		console.log("error fetching order!!!")
	});



async function getUser(){
	try{
		const user = await getUser();
		const order = await order(user.id);
		const orderDetails = await getOrderDetails(order.id);

		console.log(orderDetails);

	} catch(error=>{
		console.log("Error fetching order", error)
	})

}



Q14) What are the core modules of Node.js?

	fs - File System - Read/Write files
	http - HTTP - Create web server
	path - Path - Handle File 	
	os - Operating System - CPU, Memory, OS info
	events - Events - EventEmitter
	stream - Streams - Handle large data/files
	crypto - Cryptography - Hashing, encryption
	buffer - Binary data - Handle raw binary data
	url - URLs - Parse/manipulates


The FS:- module is used to work with the files and directories.

	Available methods: 
		Read File files
		Write files
		Update files
		Delete Files
		Create Directories
		Watch Files for changes

const fs = require("fs");

fs.readFile("data.txt", "utf", (req, res)=>{

	console.log(res);
})



The HTTP: Node.js provides the in-built http module to create HTTP servers

const http = require("http");

http.createServer((req, res)=>{
	res.writeHead(200, {
	"Content-Type": "text/plain"
	});

	res.send("Welcome to Nodejs server!!!");
})

http.listen(3000, ()=>{
	console.log("App is listening to 3000");
});



Q15) What is callback?

.) Callback is an asynchronous equivalent for a function. A callback function is called at the completion of a given task.
.) A callback is a function that is passed to another function as an argument, so it can be called later with a particular operation is finished or an event 
	happened.

Q16: How Node prevents blocking code?
Node.js uses callback function. Callback function get called whenever corresponding event triggered.

Q17. What is Event Loop?

The event loop is an mechanism that helps Node.js handle asynchronous operations without blocking the main thread.
First normal JavaScript code is executed in the Call Stack. When Node.js encounters a asynchronous operation, 
such as timer, file operation , or API request, it handles that operation outside the Call Stack. Once the operation is completed,
it's callback is placed in a queue. The Event Loop continuously checks whether the Call Stack is empty. If it is empty, the Event Loop moves the callback from the queue to the Call Stack, where it gets executed.

1. Synchronous code
        ↓
2. process.nextTick()       ← Node.js
        ↓
3. Microtasks
   - Promise.then()
   - queueMicrotask()
        ↓
4. Macrotask / Event Loop phase
   - setTimeout()
   - setInterval()
   - I/O callbacks
   - setImmediate()
        ↓
5. Microtasks again
        ↓
6. Next macrotask
        ↓
   Repeat 🔄


Synchronous code runs first, then Node's process.nextTick() queue and microtask are processed , and then the Event Loop executes eligible
macrotasks. After a callback.


Q18)


setTimeout()
------------

setTimeout(() => {
    console.log("Hello");
}, 2000);

Run code after a minimum delay

setTimeout() is used to schedule a callback to run after a specified delay.


setInterval()
-------------

setInterval(() => {
    console.log("Running...");
}, 1000);

Run code repeatedly

setInterval() is used to repeatedly execute a callback at a specified interval until the timer is cancelled.


setImmediate()
--------------
Schedule a callback to execute during the check phase of Node.js's Event Loop.
 
setImmediate(() => {
    console.log("Immediate");
});

setImmediate() schedules a callback to run in the check phase of the Node.js Event Loop, after the poll phase.


process.nextTick()
------------------

Execute a callback after the current operation finishes but before the Event Loop continues to its next phase.


console.log("Start");

process.nextTick(() => {
    console.log("Next Tick");
});

console.log("End");

process.nextTick() schedules a callback to run after the current operation completes, before the Event Loop proceeds to the next phase.



Q19) What is EventEmitter?

EventEmitter is a class provided by Node.js events module that allows us to create, emit, and listen events. We use emit to trigger an event and on to register a listener that responds to that event.

this is used to Streams and networking.

on() - Listen
emit() - Trigger


Q20) What is buffer class in Node.js?

Buffer class is a global class and it can be accessed in application without importing buffer module. A buffer is a kind of Array of integers and corresponds to a raw memory allocation outside V8 heap

- It can not be resized.

Q21)  ChildProcess Module?
	
A child_process is a module used to create new processes. The two methods are spawn() and fork() and the cluster module builds a multi process server application.

child_process.spawn() : - 
