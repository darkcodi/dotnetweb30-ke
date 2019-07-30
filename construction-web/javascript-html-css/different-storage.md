# Different storage

### Cookies

Cookies are data, stored in small text files, on your computer.

When a web server has sent a web page to a browser, the connection is shut down, and the server forgets everything about the user.

Cookies were invented to solve the problem "how to remember information about the user":

* When a user visits a web page, his/her name can be stored in a cookie.
* Next time the user visits the page, the cookie "remembers" his/her name.

Cookies are saved in name-value pairs like: **username = John Doe**

When a browser requests a web page from a server, cookies belonging to the page are added to the request. This way the server gets the necessary data to "remember" information about users.

JavaScript can create, read, and delete cookies with the `document.cookie` property.

With JavaScript, a cookie can be created like this: ****

```javascript
document.cookie = "username=John Doe";
```

You can also add an expiry date \(in UTC time\). By default, the cookie is deleted when the browser is closed: 

```javascript
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC";
```

With a path parameter, you can tell the browser what path the cookie belongs to. By default, the cookie belongs to the current page. 

```javascript
document.cookie = "username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/";
```

With JavaScript, cookies can be read like this:

```javascript
var x = document.cookie;
```

{% hint style="info" %}
`document.cookie` will return all cookies in one string much like: cookie1=value; cookie2=value; cookie3=value;
{% endhint %}

With JavaScript, you can change a cookie the same way as you create it:

```javascript
document.cookie = "username=John Smith; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/";
```

The old cookie is overwritten.

Deleting a cookie is very simple.

You don't have to specify a cookie value when you delete a cookie.

Just set the expires parameter to a passed date:

```javascript
document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/;";
```

{% hint style="info" %}
You should define the cookie path to ensure that you delete the right cookie.

Some browsers will not let you delete a cookie if you don't specify the path.
{% endhint %}

The `document.cookie` property looks like a normal text string. But it is not.

Even if you write a whole cookie string to document.cookie, when you read it out again, you can only see the name-value pair of it.

If you set a new cookie, older cookies are not overwritten. The new cookie is added to document.cookie, so if you read document.cookie again you will get something like:

cookie1 = value; cookie2 = value;

If you want to find the value of one specified cookie, you must write a JavaScript function that searches for the cookie value in the cookie string.

### Web storage \(local and session\)

With web storage, web applications can store data locally within the user's browser.

Before HTML5, application data had to be stored in cookies, included in every server request. Web storage is more secure, and large amounts of data can be stored locally, without affecting website performance.

Unlike cookies, the storage limit is far larger \(at least 5MB\) and information is never transferred to the server.

Web storage is per origin \(per domain and protocol\). All pages, from one origin, can store and access the same data.

HTML web storage provides two objects for storing data on the client:

* `window.localStorage` - stores data with no expiration date
* `window.sessionStorage` - stores data for one session \(data is lost when the browser tab is closed\)

Before using web storage, check browser support for localStorage and sessionStorage:

```javascript
if (typeof(Storage) !== "undefined") {
  // Code for localStorage/sessionStorage.
} else {
  // Sorry! No Web Storage support..
}
```

The localStorage object stores the data with no expiration date. The data will not be deleted when the browser is closed, and will be available the next day, week, or year.

```javascript
// Store
localStorage.setItem("lastname", "Smith");

// Retrieve
document.getElementById("result").innerHTML = localStorage.getItem("lastname");
```

Example explained:

* Create a localStorage name/value pair with name="lastname" and value="Smith"
* Retrieve the value of "lastname" and insert it into the element with id="result"

The example above could also be written like this:

```javascript
// Store
localStorage.lastname = "Smith";
// Retrieve
document.getElementById("result").innerHTML = localStorage.lastname;
```

The syntax for removing the "lastname" localStorage item is as 

```javascript
follows:localStorage.removeItem("lastname");
```

**Note:** Name/value pairs are always stored as strings. Remember to convert them to another format when needed!

{% hint style="success" %}
 The `sessionStorage` object is equal to the localStorage object, **except** that it stores the data for only one session. The data is deleted when the user closes the specific browser tab.
{% endhint %}



