# 10.2.3 `intersection`

您可以使用 `intersection` 函数找到与直线以最短距离相交的点，或查找通过的直线与另一条直线的最短距离相交。

### 描述

如果您指定两点形成一条直线和另一点作为参数，您将获得一条连接直线和一个点的交叉位置，且该位置的距离最短。

![](../../_assets/image_intersection_1.png)

如果您指定两点形成一条直线和两点形成另一条直线作为参数，您可以找到这两条直线的最短距离交点。交点是您指定的第一条直线的交点。

![](../../_assets/image_intersection_2.png)


### 语法

```python
result=intersection(<straight-line ref.pose 1>,<straight-line ref.pose 2>,<position ref.pose>)
```

```python
result=intersection(<straight-line ref.pose 1>,<straight-line ref.pose 2>,<straight-line ref.pose 3>,<straight-line ref.pose 4>)
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
      <td style="text-align:left">straight-line ref.pose 1</td>
      <td style="text-align:left">
        第一条直线的第一个参考姿态
      </td>
      <td style="text-align:left">姿态表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 2</td>
      <td style="text-align:left">
        第一条直线的第二个参考姿态
      <td style="text-align:left">姿态表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">position ref.pose</td>
      <td style="text-align:left">
        用于查找直线和最短距离位置的姿态
      </td>
      <td style="text-align:left">姿态表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 3</td>
      <td style="text-align:left">
        第二条直线的第一个参考姿态
      </td>
      <td style="text-align:left">姿态表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">straight-line ref.pose 4</td>
      <td style="text-align:left">
        第二条直线的第二个参考姿态
      </td>
      <td style="text-align:left">姿态表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
     var po1,po2,po3,result
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000)
     po2=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000)
     po3=Pose(2500.000,500.000,1938.000,0.000,0.000,0.000)
     result=intersection(po1,po2,po3)
     end
```

```python
     var po1,po2,po3,po4,result
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000)
     po2=Pose(1500.000,500.000,1938.000,0.000,0.000,0.000)
     po3=Pose(2000.000,0.000,2000.000,0.000,0.000,0.000)
     po4=Pose(2000.000,0.000,2000.000,0.000,0.000,0.000)
     result=intersection(po1,po2,po3,po4)
     end
```