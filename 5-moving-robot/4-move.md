# 5.4 `移动 (move)`

`移动 (move)` 语句是用于移动机器人的过程。格式如下。

### 描述

机器人的工具尖端移动到姿态位置。

### 语法

move &lt;插值&gt;, \[tg=&lt;姿态/偏移&gt;\], spd=&lt;速度&gt;, accu=&lt;精度&gt;

, tool=&lt;工具编号&gt; \[x=&lt;赋值语句&gt;,\] \[直到 &lt;条件表达式&gt;\]

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
      <td style="text-align:left">插值</td>
      <td style="text-align:left">
        <p>P: 轴插值;</p>
        <p>L: 线性插值;</p>
        <p>C: 圆形插值;</p>
        <p>SP: 静态轴插值;</p>
        <p>SL: 静态工具线性插值;</p>
        <p>SC: 静态工具圆形插值</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">姿态/偏移</td>
      <td style="text-align:left">
        <p>要移动到的目标姿态（pose）</p>
        <p>如果存在隐藏姿态，将被省略。</p>
        <p>如果以 + 或 - 符号指定了偏移表达式，将会应用（隐藏姿态 + 
          偏移表达式）作为目标姿态。</p>
      </td>
      <td style="text-align:left">姿态表达式或带符号的偏移表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">速度</td>
      <td style="text-align:left">
<p>工具尖端的移动速度</p>
<p>应该添加一个单位（mm/秒，cm/分钟，秒，%）。</p>
</td>
<td style="text-align:left">算术表达式</td>
</tr>
<tr>
<td style="text-align:left">准确性</td>
<td style="text-align:left">
<p>算术表达式</p>
<p>值越低，越准确。如果为0，则操作将不连续地发生。</p>
</td>
<td style="text-align:left">0~7</td>
</tr>
<tr>
<td style="text-align:left">工具编号</td>
<td style="text-align:left">机器人操作时使用的工具编号</td>
<td style="text-align:left">0~31</td>
</tr>
<tr>
<td style="text-align:left">赋值语句</td>
<td style="text-align:left">
<p>当移动开始时，将按从左到右的顺序执行赋值语句。</p>
</td>
<td style="text-align:left">如果不为0则为真，如果为0则为假
<p>"&lt;赋值语句1;赋值语句2;...&gt;"<\p>
</td>
</tr>
<tr>
<td style="text-align:left">条件表达式</td>
<td style="text-align:left">
<p>一旦条件表达式为真，机器人操作将结束，指定的姿势将被视为已达到。</p>
<p>条件表达式的结果可以通过result()函数获得。</p>
</td>
<td style="text-align:left">如果不为0则为真，如果为0则为假</td>
</tr>
</tbody>
</table>

### 示例

```python
move L,tg=po[0]+sft[1],spd=800mm/sec,accu=0,tool=1
move P,tg=+Shift(0,0,0,0,-10,0),spd=80%,accu=1,tool=3,x="do1=1;do2=2",until di2  (hidden pose)
if result() then *sensor_on
```
如果按下教学挂件的 `[Record]` 按钮，隐式姿态类型的 `移动 (move)` 语句将记录为当前机器人位置。通过将光标放在 `移动 (move)` 语句上并按下 `[Property]` 按钮，可以检查或编辑隐式姿态值。 

当按下 `[Command]` 按钮并打开 `[Motion]` 组时，选择移动菜单。因此，录制了一条姿态类型的 `移动 (move)` 语句。