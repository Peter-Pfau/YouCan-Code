#  Save JSON File
## Node js Server Example

### Example
![image](https://github.com/user-attachments/assets/1fa0127b-69d0-45c2-9515-e16b2c07dd75)


### HTML 
#### index.html
```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Send JSON to Server</title>
</head>
<body>
    <h1>Send JSON to Server</h1>
    <form id="jsonForm">
        <label for="jsonInput">JSON Data:</label><br>
        <textarea id="jsonInput" rows="10" cols="50"></textarea><br>
        <button type="submit">Send</button>
    </form>

    <script>
        document.getElementById('jsonForm').addEventListener('submit', function(event) {
            event.preventDefault();
            const jsonData = document.getElementById('jsonInput').value;
            fetch('http://127.0.0.1:3000', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                    
                },
                body: jsonData
            })
            .then(response => response.text())
            .then(data => alert(data))
            .catch(error => console.error('Error:', error));
        });
    </script>
</body>
</html>
```

### JavaScript
#### nodeSaveFileServer.js

```JavaScript
const http = require('http');
const fs = require('fs');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  // Add CORS headers
  res.setHeader('Access-Control-Allow-Origin', '*');
  res.setHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE, OPTIONS');
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type, Authorization');

  if (req.method === 'OPTIONS') {
    res.statusCode = 204;
    res.end();
    return;
  }

  if (req.method === 'POST' && req.headers['content-type'] === 'application/json') {
    let body = '';
    req.on('data', chunk => {
      body += chunk.toString();
    });
    req.on('end', () => {
      fs.writeFile('data.json', body, (err) => {
        if (err) {
          res.statusCode = 500;
          res.setHeader('Content-Type', 'text/plain');
          res.end('Failed to save data\n');
        } else {
          res.statusCode = 200;
          res.setHeader('Content-Type', 'text/plain');
          res.end('Data saved successfully\n');
        }
      });
    });
  } else {
    res.statusCode = 400;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Invalid request\n');
  }
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

```
