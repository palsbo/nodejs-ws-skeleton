# Node.js Web socket skeleton sample.
## Server
All functions of the server is included in the file serverbase.js

Define object:

    var ww = new serverbase({ port: 82, dir: __dirname + '/web' });

In this example, the webserver is on port 82, and the websocket server is on the same server and the same port.

	var ww = new serverbase({ port: 82, 'url': 'localhost:83', dir: __dirname + '/web' });

In this example, the webserver is on port 82, and the websocket server is on localhost port 83.

To handle a parameter in the webrequest url (http://myserver.com?url=http:yourserver.com) :

    ww.onparm('url', function (doc, data) {     //  action if url contains parameter 'url' returns document requested and value of parameter
        console.log("Value of parameter 'url' in page '%s' is '%s'", doc, data);
    })

To handle an incoming websocket value ('url' = 'http://server.com'):

    ww.on('url', bcurl);    //  action if websocket receives 'url' parameter.

(bcurl is called with the parameter of the value of 'http://server.com')

To get callback when webserver starts listening:

    ww.on('listen', function (webport) {   //  action when web-server start to listen.
        console.log('Listening on port %s', webport);
        bcurl("http://live-icy.gss.dr.dk:8000/A/A04H.mp3");
    })

To handle an incoming webserver request:

    ww.on('connect', function (ws) {    //  action when a web-client is connected. the socket object is returned
        console.log("Now connected - sending %s", currentUrl);
        ws.send(JSON.stringify({ 'url': currentUrl, 'info': "Welcome to webradio" }));
    })

To broadcast message to all connected websocket clients:

    ww.broadcast(JSON.stringify({ 'url': currentUrl, 'info': "New url broadcasted" }));

## Client

Using the module 'websocket.js' gives auto-connect if server disconnect.
register the websocket object as this:

	var ws = new WEBSOCKET(url)
