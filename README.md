# HackYourFuture

HYF Class26 Extra Class

## Topics

- APIs
- Promises
- JSON

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

## Promises
