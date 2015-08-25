
[mailjet]: http://www.mailjet.com
[api_credential]: https://app.mailjet.com/account/api_keys
[eventemitter]: https://nodejs.org/api/events.html
[doc]: http://dev.mailjet.com/
[stable]: https://github.com/mailjet/mailjet-apiv3-nodejs

![alt text](http://cdn.appstorm.net/web.appstorm.net/files/2012/02/mailjet_logo_200x200.png "Mailjet")

# Mailjet EcmaScript2015 Wrapper

Please welcome the new [Mailjet][mailjet] experimental EcmaScript API wrapper!
If you want a Stable ES5 version, click [Here][stable]

It is basically a translation, implementing the new EcmaScript specifications.

[Mailjet][mailjet] is an Email Service Provider (ESP). Visit the website and get comfortable!

For more details, see the full [API Documentation][doc]

## Getting started

first, create a project folder

`mkdir mailjet-project && cd $_`

### Installation

if you want to get a global installation, you can add `-g`

`npm install mailjet-next`



### Show me the code

To authenticate, go get your API key, and API secret [here][api_credential],
open your favorite text editor and import the mailjet module

``` javascript

import MailjetClient from 'mailjet-next';

let mailjet = new Mailjet('apiKey', 'apiSecret');

```

### Get cosy with Mailjet


#### Save your `API_KEY` and `API_SECRET`:

`echo 'export MJ_APIKEY_PUBLIC=MY_API_KEY' >> ~/.zshrc`

`echo 'export MJ_APIKEY_PRIVATE=MY_API_SECRET' >> ~/.zshrc`

`source ~/.zshrc`

replace `zshrc` with `bash_profile` if you are simply using bash

#### And use it in your projects

``` javascript

const apiKey = process.env.MJ_APIKEY_PUBLIC;
const apiSecret = process.env.MJ_APIKEY_PRIVATE;

```

### Store a Mailjet resource

``` javascript

// GET resource
let user = Mailjet.get('user');

// POST resource
let sender = Mailjet.post('sender');

```

### Request your resource with a callback function

``` javascript

user.request((error, response, body) => {
	if (error)
		console.log (`Oops, something went wrong ${response.statusCode}`);
	else
		console.log (body);
});

```

### Make the same request with a Promise

the request method actually returns a [EventEmitter][eventemitter] triggering `success` and `error`

``` javascript

user.request()
	.then((response) => {

	}, (error) => {

	});

```

### Pass data to your requests

``` javascript

sender
	.request({ Email: 'mr@mailjet.com' })
	.then(handleData, handleError);

```

### Pass parameters as well as a callback

``` javascript

let getContacts = Mailjet.get('contact');

getContacts.request({Limit: 3}, handleContacts);

```

### Request a resource with an ID

``` javascript

getContacts
	.id(2)
	.request(handleSingleContact);

````

### Request a ressource with an Action

``` javascript

var postContact = Mailjet.post('contact');

postContact.action('managemanycontacts')
	.request({ContactLists, Contacts})
	.then(handleData, handleError);

```

### Send an Email

``` javascript

var sendEmail = Mailjet.post('send');

var emailData = {
    'FromEmail': 'my@email.com',
    'FromName': 'My Name',
    'Subject': 'Test with the NodeJS Mailjet wrapper',
    'Text-part': 'Hello NodeJs !',
    'Recipients': [{'Email': 'roger@smith.com'}],
}

sendEmail
	.request(emailData)
    .then(handleData, handleError);

```

### Send two Emails

``` javascript

var emailData = {
    'FromEmail': 'gbadi@student.42.fr',
    'FromName': 'Guillaume badi',
    'Subject': 'Coucou Mailjet2',
    'Text-part': 'Hello World2',
    'Recipients': [{'Email': 'gbadi@mailjet.com'}],
}

var emailData2 = emailData;
emailData2['Text-part'] = 'This is another Email';

sendEmail
	.request(emailData)
    .then(handleData, handleError);

sendEmail
	.request(emailData2)
    .then(handleData, handleError);

```

## Contribute

Mailjet loves developers. You can be part of this project!

This wrapper is a great introduction to the open source world, check out the code!

Feel free to ask anything, and contribute:

- Fork the project.
- Create a new branch.
- Implement your feature or bug fix.
- Add documentation to it.
- Commit, push, open a pull request and voila.

TODO:

- Add compatibility with `duplicatefrom` filter
