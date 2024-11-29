# Node JS Server Examples

## Create Server and req.url
```JavaScript
var http = require('http') //import Node.js core module
var server = http.createServer(function(req, res){

    if (req.url == '/'){ //check the URL fo the current

        // set response header

        res.writeHead(200,{ 'Content-Type': 'text/html'});

        // set response content

        res.write('<html><body><p>This is home page.</p><script>console.log("IN THE BROWSER")</script></body></html>');

        console.log("IN THE SERVER");

        res.end();

    }

    else if (req.url == "/student") {

        res.writeHead(200,{ 'Content-Type': 'text/html'});

        // set response content

        res.write('<html><body><p>This is the student home page.</p><script>console.log("This is student home page IN THE BROWSER")</script></body></html>');

        console.log("IN THE Student SERVER");

        res.end();

    }

    else if (req.url == "/admin") {

        res.writeHead(200,{ 'Content-Type': 'text/html'});

        // set response content

        res.write('<html><body><p>This is admin home page.</p><script>console.log("This is admin home page")</script></body></html>');

        console.log("IN THE ADMIN SERVER");

        res.end();
    }
    else
        res.end('Invalid Request');
});

server.listen(5000); //6 - listen for any incoming requests
console.log('Node.js web server at port 5000 is running');
```
