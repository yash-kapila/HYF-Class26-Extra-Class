# HackYourFuture

HYF Class26 Extra Class

## Topics

- APIs
- JSON
- Promises

## Application Programming Interface(API)

An API as the name suggests is an **interface** which we can use in order to establish a connection between our application and an external system, application or a library.

We have been dealing with **interfaces** ever since we have owned a computer. For example, we use a _Graphical User Interface(GUI)_ to interact with different applications or operating system running on our computer. Additionally, we make use of a _Command Line Interface(CLI)_ to interact with the OS's file system. For example, you have already been using the CLI to work with Git for your homework submissions.

The above description of interfaces imply that you have already been working with interfaces(perhaps without realising it). APIs are no different. An API, in comparison to GUI or CLI, is a **software-to-software interface** and not a **user interface**. This means that using APIs, different applications talk to each other without any user knowledge or intervention.

Such communication can be categorised into different scenarios:
1. Frontend-Backend
2. Intra-Frontend

### Frontend-Backend

This is perhaps the most common interaction between applications in web development world and what many people refer to when using the term APIs.

Have you ever imagined how do you see all the latest posts or tweets on Instagram or on Twitter? Or when you login to your banking app, how do you see all your accounts and transactions for those accounts? Or when you go to an e-commerce application, how is it that all available items are listed in front of you? - all this is done using the magic of APIs.

Somewhere on the backend server, there is an application running exposing some functions which a frontend application can connect to exchange information. For example, you can imagine that a function is executed on GitHub server when you were trying Week1's homework and connecting to `https://api.github.com/orgs/HackYourFuture/repos?per_page=100`

And how do we connect to this API from our frontend application is making use of [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) or [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).

#### Examples

```javascript
const HYF_URL = `https://api.github.com/orgs/HackYourFuture/repos?per_page=100`;

fetch(HYF_URL)
	.then(response => response.json())
	.then(data => {
		console.log(`Data returned from GitHub API is: ${data}`);
	});
```

```javascript
const HYF_URL = `https://api.github.com/orgs/HackYourFuture/repos?per_page=100`;

const xhr = new XMLHttpRequest();
xhr.open('GET', HYF_URL);
xhr.responseType = 'json';
xhr.onload = () => {
	console.log(`Data returned from GitHub API is: ${data}`);
};
xhr.send();
```

This will make more sense when you get to NodeJS module and create your own server-side APIs. :smiley:

### Intra-Frontend

While the term API is most commonly used for the first scenario, it is also applicable for an intra-application communication. Actually, we have been using APIs already without noticing. 

The functions which you have used so far such as:

- `addEventListener`
- `setTimeout`
- `requestAnimationFrame`
- `XMLHttpRequest`
- `fetch`

are all APIs provided by the browser which we use in our frontend application.

Similarly, you can create your own APIs and use it within your application. We do it by making use of modules which we learnt in JS3 Week1.

#### Examples

Example1: Plain JavaScript modules interacting with each other using APIs

```JavaScript
/* utils.js */
const utils = () => ({
  /* sum and multiply are APIs exposed by utils.js */
  sum: (...params) => params.reduce((elem, acc) => elem + acc, 0),
  multiply: (...params) => params.reduce((elem, acc) => elem * acc, 1);
});

export default utils;


/* app.js */
import utils from 'utils';

/* A different program app.js now uses APIs exposed by utils */
const main = () => {
  console.log(`Summing numbers: ${utils.sum(1,2,3,4)}`);
  console.log(`Multiplying numbers: ${utils.multiply(1,2,3,4)}`);
};

main();
```

## JSON

In a typical web application, there is always a communication required between client(browser) and server(just another computer running a program). While we write client side applications using JavaScript, the program running on the server can be written in any other language(Java, .NET, PHP etc).

Thus, in order for both programs to communicate(using APIs :wink:), there should be a method which is understandable by both. Previously, XML used to be one of the ways of sharing information between client and server. But nowadays, JSON is considered as a preferable way of communicating and exchanging information.

JavaScript Object Notation (JSON) is a standard text-based format for representing structured data based on _JavaScript object_ syntax. Even though it closely resembles JavaScript object literal syntax, it can be used independently from it.

### Example

```json
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": [
        "Radiation resistance",
        "Turning tiny",
        "Radiation blast"
      ]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```

If you open https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json in the browser, you will see response coming in a JSON format.

This means is that there is a program running on a machine which is reachable via mdn.github.io and when it receives a request `learning-area/javascript/oojs/json`, it executes a function which returns us the JSON we see on browser.

### JSON Manipulations

Sometimes, there are situations when we receive a raw JSON as a string or need to convert a JSON to a string for easy transfer among programs. Thus, JavaScript provides a global JSON object which provides two methods to fulfil the purpose.

- `parse()` - Accepts a JSON string as a parameter, and returns the corresponding JavaScript object.
- `stringify()` - Accepts an object as a parameter, and returns the equivalent JSON string form.

### Notes:

- JSON is purely **a data format** — it contains only properties, no methods.
- JSON requires double quotes to be used around strings and property names. Single quotes are not valid.
- Even a single misplaced comma or colon can cause a JSON file to go wrong, and not work.

For example, below is a valid JavaScript object but not a JSON

```javascript
{
	name: 'Yash Kapila',
	age: 30,
}
```

while the following is a valid JSON

```json
{
	"name": "Yash Kapila",
	"age": 30
}
```

## Promises

### Why

Asynchronous Programming is a crucial component of web development using JavaScript. This is because JavaScript is a single threaded by nature and hence can do only one thing at a time. Without async programming, if we were to fetch some data through an API from backend, we couldn't do anything else and our web page might appear frozen.

We have already seen and used several ways to achieve asynchronous programming so far. DOM Event Listeners, setTimeout, setInterval and callbacks are different ways to achieve asynchronous programming.

A question may arise in your head asking why do we need promises when we have callbacks already for async programming in JavaScript. A good question and the answer to it lies in the following example.

Imagine, you have to do task A and upon its completion do task B and upon B's completion, do task C and so on. Our code might look like this:

```javascript
finishTaskA(function(err, done) {
	if (err) {
		console.log('Error');
	} else {
		finishTaskB(function(err, done) {
			if (err) {
				console.log('Error');
			} else {
				finishTaskC(function(err, done) {
					if (err) {
						console.log('Error');
					} else {
						// and so on
					}
				});
			}
		})
	}
})
```

Needless to say but you can see how ugly this code is and uglier it can soon get. This is also known as **callback hell** or **callback pyramid**.

Let's see how this could might look if we used promises instead:

```javascript
finishTaskA()
	.then(function() {
		return finishTaskB();
	})
	.then(function() {
		return finishTaskC();
	})
	.catch(function(err) {
		console.log('Error');
	})
```

We can surely compare the two approaches and tell which is perhaps easier and less prone to bugs.

### What

### How