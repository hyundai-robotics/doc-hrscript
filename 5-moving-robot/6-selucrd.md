# 5.6 `selucrd` - 选择用户坐标系统

`selucrd` 语句是一个用于更改指定为条件设置中的用户坐标系统的用户坐标系统编号的过程。

### 描述

与在条件设置中指定用户坐标系统相对应的功能。

### 语法

```python
selucrd <坐标系统编号>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">坐标系统编号</td>
      <td style="text-align:left">
        要选择的坐标系统编号<br>
        <ul>
        <li>0：取消指定用户坐标系统</li>
        <li>1~20：指定用户坐标系统</li>
        </ul>
      </td>
      <td style="text-align:left">表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   selucrd 1
   end
```