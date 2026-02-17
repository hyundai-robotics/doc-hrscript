# 5.5 `mkucs` - 创建用户坐标系

### 描述

一个创建用户坐标系的命令，使用三个姿态或一个姿态。

- 当使用三个姿态创建时，按照指定的步骤顺序创建原点姿态、轴姿态和平面姿态。
- 如果没有指定步骤顺序，则使用原点姿态、X轴姿态和XY平面姿态进行创建。
- 当使用一个姿态创建时，创建原点姿态，位置/方向基于姿态值。
- 如果无法进行计算，则作业执行会由于错误而中断。

### 语法

```python
<result variable> = mkucs(<user coord. system number>,<step order>,<origin pose>,<axis pose>,<plane pose>)
or
<result variable> = mkucs(<user coord. system number>,<origin pose>)
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
        后台执行的结果<br>
        <ul>
        <li>0: 成功完成。</li>
        <li>-1: 创建用户坐标系失败。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">user coord. system number</td>
      <td style="text-align:left">
        要创建的用户坐标系的编号
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">步骤顺序</td>
      <td style="text-align:left">
        如果未指定，以下三个姿势的顺序将为"OXY" <br>
        （示例） <br>
        "OXY" : 原点姿势, X 轴姿势, XY 平面姿势 <br>
        "OYZ" : 原点姿势, Y 轴姿势, YZ 平面姿势 <br>
      </td>
      <td style="text-align:left">字符串变量</td>
    </tr>
    <tr>
      <td style="text-align:left">原点姿势</td>
      <td style="text-align:left">
        位于原点的姿势
      </td>
      <td style="text-align:left">姿势变量</td>
    </tr>
    <tr>
      <td style="text-align:left">轴姿势</td>
      <td style="text-align:left">
        位于 X、Y、Z 轴上的姿势
      </td>
      <td style="text-align:left">姿势变量</td>
    </tr>
    <tr>
      <td style="text-align:left">平面姿势</td>
      <td style="text-align:left">
        位于 XY、YZ、ZX 平面上的姿势
      </td>
      <td style="text-align:left">姿势变量</td>
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
        OK
      </td>
<td></td>
    </tr>  
  </tbody>
</table>


### 错误

- E14613 : 当实际参数与形式参数不匹配时发生。请检查实际参数。
- E14614 : 当用户坐标编号不是数字时发生。请重新指定用户坐标编号。
- E14615 : 当用户坐标编号不是1到20之间的数字时发生。请更改用户坐标编号。
- E1011 : 当教学姿势之间的距离太近时发生。当每个点之间的距离小于1mm时发生。请纠正姿势之间的距离值。
- E1012 : 当三个调用的姿势在一条直线上时发生。


### 示例

```python
   var p_origin=Pose(0,0,0,0,0,0,"base")
   var p_xaxis=Pose(100,0,0,0,0,0,"base")
   var p_xyplane_=Pose(100,100,0,0,0,0,"base")
   var uc1 = mkucs(1,p_origin,p_xaxis,p_xyplane)
   var uc2 = mkucs(2,p_origin)
   var uc3 = mkucs(1,"OXY",p_origin,p_xaxis,p_xyplane)
   end
```

![](../../_assets/mkucs.png)