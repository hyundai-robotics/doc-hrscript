# 6.3    Http\_Cli Module: HTTP Client

Using the general-purpose Ethernet port of the Hi6 Controller makes it possible to access remote web services to receive HTTP services. 

To use this function, it is required to create an HttpCli object after importing the http\_cli module, as shown in the following example.

```python
import http_cli
var cli=http_cli.HttpCli()
```

After the HttpCli object is created, it must request a service by calling the get, put, post, and delete member procedures.

The HttpCli object has a property named “body.”

When a get service is requested and a response is received successfully, the remote server’s data will have the body property. The body property value can be a string, number, array, or object. When requesting the put service, it is required to assign the data to be transmitted to the body property in advance.

When requesting the post service, it is required to assign the data to be transmitted to the body property in advance, and the data sent as a response from the remote server is to be stored in the body property.

The delete service does not use the body property.





