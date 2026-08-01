# 5.4 `移动 (move)`

`移动 (move)` 语句是用于移动机器人的指令，其格式如下。

### 描述

机器人的工具提示移动到位姿位置。

### 语法

```python
move <插补>, [tg=<pose/shift>], spd=<速度>, accu=<精度>, tool=<工具编号> [, x=<赋值语句>] [until <条件表达式>]
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
      <td style="text-align:left">插补</td>
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
      <td style="text-align:left">速度</td>
      <td style="text-align:left">
        <p>工具提示的移动速度</p>
        <p>应添加单位（mm/sec, cm/min, sec, %）。</p>
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">精度</td>
      <td style="text-align:left">
        <p>算术表达式</p>
        <p>值越低，越准确。如果为0，操作将不连续地发生。</p>
      </td>
      <td style="text-align:left">0~7</td>
    </tr>
    <tr>
      <td style="text-align:left">工具编号</td>
      <td style="text-align:left">机器人操作时使用的工具的编号</td>
      <td
      style="text-align:left">0~31</td>
    </tr>
      <tr>
      <td style="text-align:left">赋值语句</td>
      <td style="text-align:left">
        <p>当移动开始时，将从左到右顺序执行要执行的赋值语句。</p>
      </td>
      <td style="text-align:left">True if not 0 False if 0
      <p>"&lt;assignment statement1;assignment statement2;...&gt;"<\p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">条件表达式</td>
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

如果按下示教器的 `[Record]` 按钮，则会将当前机器人的位置记录为隐藏位姿类型的 `移动 (move)` 语句。将光标放在 `移动 (move)` 语句上并按下 `[Property]` 按钮，即可查看或编辑隐藏的位姿值。

按下 `[Command]` 按钮并打开 `[Motion]` 组后，选择 move 菜单。此时，将记录一个位姿类型的 `移动 (move)` 语句。