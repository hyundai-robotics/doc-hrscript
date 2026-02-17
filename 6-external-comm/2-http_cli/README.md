# 6.2 `http_cli` Module: HTTP Client

Using the general-purpose Ethernet port of the ${cont_model} controller, it is possible to access remote web services and consume HTTP services.
To use this feature, import the `http_cli` module and create an `HttpCli` object as shown below.

```python
import http_cli
var cli = http_cli.HttpCli()
```

After creating an `HttpCli` object, service requests can be made by calling the `get`, `put`, `post`, and `delete` member procedures.<br>
The `HttpCli` object provides an attribute named `body`.<br>
- When a `GET` request is made and a response is successfully received, the data returned by the remote server is stored in the `body` attribute.<br>The type of the `body` value may be a string, a number, an array, or an object.
- When making a `PUT` request, the data to be transmitted must be assigned to the `body` attribute in advance.
- When making a `POST` request, the data to be transmitted must also be assigned to the `body` attribute in advance, and the data returned by the remote server in the response is stored in the `body` attribute.
- The `DELETE` service does not use the `body` attribute.
The provided HTTP client communication operates in synchronous mode.

