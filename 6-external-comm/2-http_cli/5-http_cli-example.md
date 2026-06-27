# 6.2.5 HTTP客户端使用示例

```python
     import http_cli
     var cli=http_cli.HttpCli()
     var url, body, query, status_code
     var domain="http://192.168.1.200:8888"

     # 获取
     cli.get domain+"/device/direction"
     body = cli.body

     #检查通信状态
     if cli.status>=400 or cli.status<0
        goto 99 		#http通信错误
     endif

     # 放置
     url = domain+"/device/direction"
     body.ry=90
     cli.body=body
     cli.put(url, 3000, *Timeout)

     # 发送
     cli.body={ name: "WORK #32", color: "green", state: "OK" }
     cli.post domain+"/display/update", 5000, *Timeout

     # 删除
     cli.delete(domain+"/items")

     end
     
  99 print "错误状态"
     
     *Timeout
     print "超时"
```