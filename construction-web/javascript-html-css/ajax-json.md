# AJAX/JSON

### AJAX 

{% hint style="info" %}
AJAX \(аббревиатура от «Asynchronous Javascript And Xml»\) – технология обращения к серверу без перезагрузки страницы.
{% endhint %}

* Свойства
  * xhr.readyState \(0-4\)
  * xhr.status
  * xhr.responseText
  * xhr.onreadystatechange
* Методы
  * `xhr.open(method, url)` 'GET', 'POST'
  * `xhr.send([data])` data только при POST запросе
  * `xhr.abort()` отменить
  * `xhr.setRequestHeader()` установить заголовок

```text
const xhr = new XMLHttpRequest();

xhr.open('GET', 'action.php');
xhr.send();

xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    console.log(xhr.responseText);
  }
}
```

### JSON <a id="json"></a>

{% hint style="info" %}
JSON - JavaScript Object Notation - который используется для представления объектов в виде строки.
{% endhint %}

* `JSON.parse(str, reviver(key, value))`
* `JSON.stringify(value, replacer, space)` \(функции игнорируются, ссылки на DOM\)

AJAX stands for Asynchronous JavaScript and XML, which sounds complicated. But using AJAX is really just using one object that comes with plain old vanilla JavaScript. This object allows you to load an external file and add its content to your webpage.

\(You can do a lot more than that, but let’s work our way up from our basic example.\)

AJAX is a way to access external files from your webpage, but it doesn’t work with files on your file system. The files you access has to be on the internet: in other words, it can’t be a `file://` you access from your own computer.

This might be annoying if all of your files have just been on your computer so far, but this is a safety feature. Imagine how scary the internet would be if any website could read files from your computer!

So if you want to try AJAX out, make sure you upload the files to a server. 

### The `onreadystatechange` Function <a id="the-onreadystatechange-function"></a>

Remember that the first A in AJAX stands for **asynchronous**. That means that your code keeps doing other stuff while the request is sent off. After all, you might be requesting a huge file that will take an hour to download! If your code had to stop everything it’s doing and wait for the file to be loaded, then during that time a visitor to your site couldn’t scroll around and click stuff. Your site would look like it was frozen.

So instead of waiting for the file to be loaded, the request is sent off and your code keeps going. Then your `onreadystatechange` function is called with updates to let you know what’s going on with the download.

#### The `readyState` Variable <a id="the-readystate-variable"></a>

The `onreadystatechanged` message is how AJAX lets your website know what’s going on with the download. Normally, the function is called 4 times:

* When AJAX establishes a connection with the server. _Hey I got directions to the file._
* When the server receives the request. _Hey I’m at the server._
* When the request is processed. _Hey I’m picking up the file now._
* When the file is loaded. _Here’s your file!_

You can check which of these states AJAX is in using the `readyState` variable. The `readyState` variable will be an integer from `1` to `4` for each of the above states, or `0` if something went wrong. _Sorry I got lost on my way to the file!_

#### The `status` Variable <a id="the-status-variable"></a>

The `readyState` variable only tells us half the story. AJAX could load the URL \(so `readyState` is `4`\), but the file might be missing \(_Hey I followed the directions you gave me, but the file wasn’t there._\), or it might require a username and a password \(_Hey I tried to get the file, but the door was locked._\), etc. So we also have to check this status, which is stored in the `status`\(surprise!\) variable.

The `status` variable holds the HTTP status code of the request. For example, it’s `200` when the URL is loaded correctly, `404` if the file is missing \(you’ve probably seen a `404` error while browsing the internet before\), or `500` if the server had an error. [Here](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) is a full list of possible values, but for now we probably only care about a `status` of `200` \(success\).

#### The `responseText` Variable <a id="the-responsetext-variable"></a>

We had to set up all of the above to make sure the file loads successfully, but we haven’t actually done anything with the content of the file yet. Finally, we can do that using the `responseText` variable.

The `responseText` variable holds the content of the file. It’s just a string value, and we can do whatever we want with it. For example, we could just set the content of one of the elements in our webpage to whatever is in the file:

```text
document.getElementById("welcome").innerHTML = ajaxRequest.responseText;
```

### JSON <a id="json"></a>

Let’s pause talking about AJAX for a second and talk about something else: JSON.

Remember that you can use object literals to represent objects in JavaScript:

```text
var point = {x: 7, y: 42};

console.log("The point is at " + point.x + ", " + point.y);
```

JSON stands for JavaScript Object Notation, and it’s a way to store data in a way that’s easy for JavaScript to understand. For example, here’s the same object stored as JSON in a string variable:

```text
var jsonString = '{"x": 7, "y": 42}';
```

If this looks weird, remember that JavaScript uses both single quotes `'` and double quotes `"` for strings. So this is just a string \(characters inside single quotes `'`\), and that string contains some double quote `"` characters.

But the string is in the JSON format, which looks a lot like an object literal, except the variable names are surrounded by double quote `"` characters. \(Actually you can do that with object literals too!\)

Now that we have a JSON string, we can use the `JSON.parse()` function to turn it into a JavaScript object that you can use in your code:

```text
var jsonString = '{"x": 7, "y": 42}';
var point = JSON.parse(jsonString);

console.log("The point is at " + point.x + ", " + point.y);
```

