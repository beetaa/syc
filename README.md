Syc
===

If you're using Javascript on both the server and client, why worry about message passing from server to client?

Syc allows you to create a variable which, when modified on the server, will reflect those same changes on the client. It works under a simple principle: All data bound to the variable in question is identical between Server and Client.

Like Meteor, but without the framework.

** Currently, Syc uses Object.observe and requires ECMA 7 on the server side to operate. Update Node.js to latest and run using the harmony flag: `node --harmony app.js` **


## Syncing a variable (Server side)

To sync a variable from the server to the client:

    var synced = new syc.sync('name')
    synced['hello'] = 'world';
    
The client will be able to access this variable by getting the reference to it:

    var synced = syc.list('name')
    synced.hello
    -> "world"

## Setting up Syc

Syc utilizes socket.io but isn't a wrapper for it. So you'll have to initalize it as such:

    var io = require('socket.io').listen(80),
        syc = require('syc');

    io.sockets.on('connection', function (socket) {
      syc.connect(socket);
    });

Now syc will be able to sync variables with this client.


- - - 
This library is a work in progress. Next release features: Client -> Server synchronization, Watchers, and an Object.observe shim for non ECMA-7 clients and servers. 

Syc currently supports the primitive types numbers, strings, booleans, as well as dates and regular expressions. Syc also supports Objects, Arrays, any any recursive combination of the two. If you would like to see additional types supported by Syc, please send an email to https://github.com/siriusastrebe

