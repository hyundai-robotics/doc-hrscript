# 6.2 `http_cli`模块：HTTP客户端

使用${cont_model}控制器的一般用途以太网端口，可以访问远程 Web 服务并使用 HTTP 服务。  
要使用此功能，请导入`http_cli`模块并创建`HttpCli`对象，如下所示。

```python
import http_cli
var cli = http_cli.HttpCli()
```

创建`HttpCli`对象后，可以通过调用`get`、`put`、`post`和`删除 (delete)`成员过程发出服务请求。<br>  
`HttpCli`对象提供一个名为`body`的属性。<br>  
- 当发出`GET`请求并成功接收响应时，远程服务器返回的数据存储在`body`属性中。<br> `body`值的类型可以是字符串、数字、数组或对象。  
- 发出`PUT`请求时，必须事先将要传输的数据分配给`body`属性。  
- 发出`POST`请求时，传输的数据也必须事先分配给`body`属性，响应中远程服务器返回的数据存储在`body`属性中。  
- `DELETE`服务不使用`body`属性。  
提供的 HTTP 客户端通信在同步模式下操作。