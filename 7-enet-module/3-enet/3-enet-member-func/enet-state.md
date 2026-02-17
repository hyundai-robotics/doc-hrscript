# `状态 (state)`

### 描述

返回以太网对象的状态。

### 语法

`{ENet object}.state`

### 返回值

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
        连接中。 <br>
        （在 UDP 的情况下，即使只是 `open` 也被视为连接。<br>
         在 TCP 的情况下，仅在 `open` 后执行 `listen`、`连接 (connect)` 和 `accept` 时才被视为连接。
      </td>
      <td></td>
    </tr>
    <tr>
      <td>0</td>
      <td>已断开连接。</td>
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


### 示例

```python
var ret = enet_to_sensor.state()
```