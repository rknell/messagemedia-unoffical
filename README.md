# MessageMedia NodeJS Library
A library that allows NodeJS programmers to access MessageMedia's SOAP API.

## How to get this library for your application:

IMPORTANT! This is taken from the official messagemedia site. The offical site seems to have forgotten to push up the library and since I needed to use it for my app on heroku and did not want to embed it into the source code, I have made this. It will be unlikely to be updated and I recommend swtiching over to the official library if MessageMedia ever does push it up.

Clone the repository into your application's *node_modules* directory.
```
$ git clone https://github.com/messagemedia/messagemedia-nodejs.git messagemedia
```
**OR**

Install it as a package from **npm** (Node Package Manager).
```
$ npm install messagemedia
```

**OR**

Create a **package.json** file in the project's root directory and add **messagemedia-unofficial** as a dependency. You can refer to the one in this project's root directory. After this file is created you can run the following command...
```
$ npm install
```

Follow the sample documentation from there.

## Project directory structure:
* **/lib** MessageMedia library.
* **/test** Contains test scripts called from **/test/tests.js**.
* **/sample** Contains a sample application.
* **/node_modules** Is created after running **$ npm install**.

### This project was created using an IDE:

IDE: Eclipse Standard

Version: Kepler Service Release 2.

It is suggested that you install http://www.nodeclipse.org/ into Eclipse. This plugin allows you to interact with NodeJS from within Eclipse.

You do not need Eclipse or any IDE to use this library. You can get started with as little has 4 lines of code...

```javascript
// app.js
const mm = require('messagemedia');
mm.checkUser('userId', 'password', function(resp){
	console.log(resp);
});
```

## Sample REST based Web App:

![alt text](sample/screenshots/screenshot1.png "Screenshot 1")

To run the sample web application type the following command:

```node sample/app.js```

In **/sample** there is a sample web application that can be used to test/demonstrate the library. 

In your web-browser go to [http://localhost:3000/](http://localhost:3000/)

### Major Parts:
* **Server** (NodeJS)
* **Client** (AngularJS)

This sample uses the Express web application framework package, on the NodeJS side.

The server (NodeJS) hosts a http server which serves a single-page for a web browser to access and a REST service. The REST service acts as a translation layer allowing two-way communication between MessageMedia's WSDL based SOAP API and this NodeJS's JSON based REST API. I have chosen to use AngularJS on the client (browser) because it is feature-rich and allows easy access to REST resources on the server.

The code snippet below shows how a very simple REST interface could be made to access MessageMedia's SOAP API via this library.
```javascript
var messagemedia = require('messagemedia');

app.post('/api/checkUser', function(req, res){
  messagemedia.checkUser(req.body.userId, req.body.password, function(result){
    res.send(result);
  });
});
```

## Unit Tests:
When attempting to run **/tests.js** for the first time you must...

* Create a **config.json** file in project root directory (use the **config.template.json** file as a template)
* Run ```$ npm install nodeunit -g```
* In ```/test``` execute ```$ nodeunit tests.js```

* **TC 1:** Checking
	* **TC 1.1:** Check User. 
	* **TC 1.2:** Check Replies
	* **TC 1.3:** Check Reports
* **TC 2:** Number Blocking
	* **TC 2.1:** Get blocked numbers.
	* **TC 2.2:** Block numbers(s).
	* **TC 2.3:** Unblock numbers(s).
* **TC 3:** Confirmations
	* **TC 3.1:** Confirm Replies.
	* **TC 3.2:** Confirm Reports.
* **TC 4:** Messages
	* **TC 4.1:** Send Messages.
	* **TC 4.2:** Delete Scheduled Messages.
	
Please note: The unit tests require an active MessageMedia account in order for them to function.
