# 10.1.3 `seltool`

`seltool` 是一个更改工具编号的过程。

### 描述

工具分为附加在机器人法兰上的机器人工具和单独安装的站点工具，`seltool` 更改每种类型的工具编号。

### 语法

```python
seltool <tool number>,<tool type>
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
      <td style="text-align:left">tool number</td>
      <td style="text-align:left">
        工具编号<br>
        <ul>
        <li>机器人工具: 0 ~ 31</li>
        <li>站点工具: 0 ~ 3</li>
        </ul>
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">tool type</td>
      <td style="text-align:left">
        要更改工具编号的工具类型<br>
        <ul>
        <li>机器人工具: robot</li>
        <li>站点工具: station</li>
        </ul>
      </td>
      <td style="text-align:left">robot/station</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   move P,spd=30%,accu=0,tool=1
   seltool 0,station
   move SP,spd=30%,accu=0,tool=1
   move SL,spd=30mm/s,accu=0,tool=1
   move SL,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   end
```