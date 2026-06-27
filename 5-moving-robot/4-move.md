# 5.4 `移动 (move)`

The `移动 (move)` statement is a procedure for moving the robot. The format is as follows.

### Description

机器人的工具提示移动到位姿位置。

### Syntax

move &lt;interpolation&gt;, \[tg=&lt;pose/shift&gt;\], spd=&lt;speed&gt;, accu=&lt;accuracy&gt;

, tool=&lt;tool number&gt; \[x=&lt;assignment statement&gt;,\] \[until &lt;conditional expression&gt;\]

### Parameter

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Interpolation</td>
      <td style="text-align:left">
        <p>P: 轴插补;</p>
        <p>L: 线性插补;</p>
        <p>C: 圆形插补,</p>
        <p>SP: 静止轴插补,</p>
        <p>SL: 静止工具线性插补,</p>
        <p>SC: 静止工具圆形插补</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Pose/Shift</td>
      <td style="text-align:left">
        <p>目标姿态（位姿）移动到</p>
        <p>如果有隐藏位姿，则将被省略。</p>
        <p>如果指定了带有+或-符号的移位表达式，（隐藏位姿+移位表达式）将作为目标姿态。</p>
      </td>
      <td style="text-align:left">位姿表达式或签名移位表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">Speed</td>
      <td style="text-align:left">
        <p>工具提示的移动速度</p>
        <p>应添加单位（mm/sec, cm/min, sec, %）。</p>
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">Accuracy</td>
      <td style="text-align:left">
        <p>算术表达式</p>
        <p>值越低，越准确。如果为0，操作将不连续地发生。</p>
      </td>
      <td style="text-align:left">0~7</td>
    </tr>
    <tr>
      <td style="text-align:left">Tool number</td>
      <td style="text-align:left">机器人操作时使用的工具的编号</td>
      <td
      style="text-align:left">0~31</td>
    </tr>
      <tr>
      <td style="text-align:left">Assignment statement</td>
      <td style="text-align:left">
        <p>当移动开始时，将从左到右顺序执行要执行的赋值语句。</p>
      </td>
      <td style="text-align:left">True if not 0 False if 0
      <p>"&lt;assignment statement1;assignment statement2;...&gt;"<\p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Conditional expression</td>
      <td style="text-align:left">
        <p>一旦条件表达式为真，机器人操作将结束，指定的姿态被认为已达到。</p>
        <p>条件表达式的结果可以通过result()函数获得。</p>
      </td>
      <td style="text-align:left">True if not 0 False if 0</td>
    </tr>
  </tbody>
</table>

### Example

```python
move L,tg=po[0]+sft[1],spd=800mm/sec,accu=0,tool=1
move P,tg=+Shift(0,0,0,0,-10,0),spd=80%,accu=1,tool=3,x="do1=1;do2=2",until di2  (hidden pose)
if result() then *sensor_on
```

If the `[Record]` button of the teach pendant is pressed, a `移动 (move)` statement in hidden pose type will be recorded as the current robot position. The hidden pose value can be checked or edited by placing the cursor on the `移动 (move)` statement and pressing the `[Property]` button. 

When the `[Command]` button is pressed and the `[Motion]` group is opened, select the move menu. As a result, a pose-type `移动 (move)` statement is recorded.