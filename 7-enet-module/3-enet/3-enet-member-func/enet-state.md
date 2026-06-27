# `状态 (state)`

### Description

返回以太网对象的状态。


### Syntax

`{ENet object}.state`


### Return value

<table>
  <thead>
    <tr>
      <th style="text-align:left">名称</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        已连接。 <br>
        （在UDP的情况下，甚至仅仅是`open`也被视为已连接。<br>
         在TCP的情况下，只有在`open`之后执行`listen`、`连接 (connect)`和`accept`时才被视为已连接。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>0</td>
      <td>未连接。</td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>创建以太网套接字失败。</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>绑定以太网套接字失败。</td>
      <td></td>
    </tr>
    <tr>
      <td>-3</td>
      <td>连接失败。</td>
      <td></td>
    </tr>
    <tr>
      <td>-4</td>
      <td>监听失败。</td>
      <td></td>
    </tr>
    <tr>
      <td>-5</td>
      <td>接受失败。</td>
      <td></td>
    </tr>
  </tbody>
</table>


### Example

```python
var ret = enet_to_sensor.state()
```