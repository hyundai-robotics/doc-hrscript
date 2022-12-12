# 7.2 TCP server example

The TCP server example program is explained for the case of tranceiving string data and binary data.

While the TCP client connects to the server with the `connect()` function, the TCP server calls the `listen()` function and waits for the client's connection with the `accept()` function.  

* Allow only one client connection at the same time.
* You do not need to specify a remote port.

The rest of the action is the same as the client.