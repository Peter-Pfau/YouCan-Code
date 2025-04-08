# Fetch Request Diagaram Flow
![image](https://github.com/user-attachments/assets/fcb20116-f8f1-41bb-8bdb-1c70d46d1387)

```HTML
index.html
-----------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Button Click Example</title>
    <script src="script.js" defer></script>
</head>
<body>
    <button id="myButton">Click Me</button>
</body>
</html>
```

In the HTML file, we have a button with the ID `myButton`. When this button is clicked, it will trigger an event listener that is defined in the `script.js`.

```
script.js
----------
document.addEventListener('DOMContentLoaded', (event) => {
    const button = document.getElementById('myButton');
    button.addEventListener('click', () => {
        fetch('/button-clicked', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({ message: 'Button was clicked' })
        })
        .then(response => response.json())
        .then(data => {
            console.log('Success:', data);
        })
        .catch((error) => {
            console.error('Error:', error);
        });
    });
});
```

In the JavaScript file `script.js`, we add an event listener to the button. When the button is clicked, a `POST` request is sent to the `/button-clicked` route on the server. The request contains a simple JSON payload.

```
server.js (Node.js with Express)
--------------------------
const express = require('express');
const app = express();
const port = 3000;

app.use(express.json());

app.post('/button-clicked', (req, res) => {
    console.log(req.body);
    res.json({ message: 'Button click received' });
});

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}/`);
});
```

In the `server.js` file, we create a Node.js server using the Express framework. The server listens for `POST` requests at the `/button-clicked` route. When a request is received, the server logs the request body and responds with a JSON message.

### Diagram Flow:
1. **index.html**: Render a button on the webpage.
2. **script.js**: Add an event listener to the button to listen for click events.
3. **Button Click**: When the button is clicked, the event listener sends a `POST` request to the server.
4. **server.js**: Handle the `POST` request on the server and send a response back to the client.

This is a simplified overview of the interactions and flow of data between the three files when the button is clicked.


The `<script>` tag is used to include JavaScript code in your HTML document. The `src` attribute specifies the URL of an external script file (`script.js` in this case).

The `defer` attribute is a Boolean attribute that tells the browser to execute the script after the document has been parsed. Here is a detailed explanation of each part of `<script src="script.js" defer></script>`:

1. **`<script>`**: This tag specifies that you are including a script in your HTML document. 

2. **`src="script.js"`**: This attribute specifies the path to the external JavaScript file (`script.js`) that you want to include. The browser will fetch and execute this script.

3. **`defer`**: This is a Boolean attribute that indicates to the browser that the script should be executed in the order it is found in the document, but only after the HTML document has been completely parsed. Here are some key points about the `defer` attribute:
   - The script is downloaded in the background during the HTML parsing process, but it will not be executed until the parsing is complete.
   - This is useful for scripts that operate on elements on the page (like adding event listeners), because it ensures that the DOM is fully built before the script runs.
   - Unlike the `async` attribute, `defer` maintains the order of execution according to their location in the document.
   
In summary, using `<script src="script.js" defer></script>` ensures that your `script.js` file will load in the background while the HTML is being parsed, and it will execute only after the entire HTML document has been parsed. This can help improve the performance and reliability of your web page, especially if your JavaScript depends on DOM elements that need to be fully loaded before being manipulated or accessed.

Here is the typical order of execution with `defer`:

- Browser begins fetching `script.js` as soon as it encounters the `<script>` tag.
- The HTML document continues to be parsed while the script is being fetched.
- Once the HTML document has been fully parsed, the `script.js` is executed in the order it was found in the document, ensuring that all DOM elements are available for the script to interact with.

This is especially useful when dealing with JavaScript that needs to interact with or manipulate the DOM, as it avoids errors that can occur if the script runs before the DOM is fully loaded.


![image](https://github.com/user-attachments/assets/205fb949-3d0d-4b90-a7ca-b65ef30eb4c0)



