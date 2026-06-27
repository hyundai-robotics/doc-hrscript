# 10.2.1 `rducs` - 用户坐标系

### 描述

读取生成的用户坐标系作为姿态的功能。

- 将创建的用户坐标系的位置/方向复制到其姿态值中。
- 如果未创建或参数无效，将以错误中断作业执行。

### 语法

```python
<result variable> = rducs(<user coord. system number>,<pose variable>)
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
      <td style="text-align:left">result variable</td>
      <td style="text-align:left">
        背景执行的结果<br>
        <ul>
        <li>0: 成功完成。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">user coord. system number</td>
      <td style="text-align:left">
        要读取的用户坐标系的编号
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">pose variable</td>
      <td style="text-align:left">
        获取位置/方向的变量
      </td>
      <td style="text-align:left">姿态变量</td>
    </tr>
  </tbody>
</table>

### 返回值

<table>
  <thead>
    <tr>
      <th style="text-align:left">值</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        确定
      </td>
      <td></td>
    </tr>  
  </tbody>
</table>

### 错误

- E14613 : 当实际参数与形式参数不匹配时发生。检查实际参数。
- E14614 : 当用户坐标编号不是数字时发生。请重新指定用户坐标编号。
- E14615 : 当用户坐标编号不在1到20之间时发生。请更改用户坐标编号。
- E1336 : 如果这是未注册的用户坐标编号，则发生。请更改用户坐标编号。

### 示例

```python
   var p_uc2=Pose(0,0,0,0,0,0,"base")
   var res=rducs(2,p_uc2)
   end
```