# 10.2.2 `segment`

`segment` 是将起始位置和结束位置之间的距离均匀划分的函数。


### 描述

将函数因子之间的起始位置和结束位置的距离均匀划分，并根据指定计数器存储考虑到位置和姿态的姿态值。
![](../../_assets/image_segment_1.png)

例如，如果 `P3=segment(P1,P2,3,2)`，则将 `P1` 起始位置与 `P2` 目标位置之间的距离划分为 3 个相等部分，并将第二个姿态的位置和旋转的姿态值存储在 `P3` 姿态变量中。

当您将经过位置作为函数的参数添加时，组成起始位置、经过点和目标位置的弧上的距离被均匀划分，位置和旋转的姿态值存储在姿态变量中。

![](../../_assets/image_segment_2.png)

例如，如果 `P10=segment(P1,P2,P3,4,2)`，
则组成 `P1` 起始姿态和 `P2` 经过姿态 `P3` 目标姿态的弧上的距离被划分为 4 个相等部分，指定第二个姿态的位置和旋转的姿态值存储在 `P10` 姿态变量中。

<br>

### 语法

```python
result=segment(<start pose>,<end pose>,<division number>,<counter>)
```

```python
result=segment(<start pose>,<via pose>,<end pose>,<division number>,<counter>)
```

### 返回值

结果姿态。

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
      <td style="text-align:left">start pose</td>
      <td style="text-align:left">
        start pose
      </td>
```html
<td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">经过姿态</td>
      <td style="text-align:left">
        经过姿态
      <td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">结束姿态</td>
      <td style="text-align:left">
        结束姿态
      </td>
      <td style="text-align:left">姿态表达</td>
    </tr>
    <tr>
      <td style="text-align:left">分割数</td>
      <td style="text-align:left">
        分割数<br>
        (1 ~ 30000)
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">计数器</td>
      <td style="text-align:left">
        要存储的姿态计数器编号<br>
        (0 ~ 300000, 0: 起始姿态)
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
  </tbody>
</table>

### 示例
```python
     var po1,po2,po3
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # 起始姿态
     po2=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # 结束姿态
     po3=segment(po1,po2,4,2)
     end
```

```python
     var po1,po2,po3,po10
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # 起始姿态
     po2=Pose(1500.000,500.000,1938.000,0.000,0.000,0.000) # 经过姿态
     po3=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # 结束姿态
     po10=segment(po1,po2,po3,5,3)
     end
```
