# 5.4 move

The move statement is a procedure for moving the robot. The format is as follows.

### Description

The robot’s tool tip moves to the pose position.

### Syntax

move &lt;interpolation&gt;, \[tg=&lt;pose/shift&gt;\], spd=&lt;speed&gt;, accu=&lt;accuracy&gt;

, tool=&lt;tool number&gt; \[until &lt;conditional expression&gt;\]

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
        <p>P: Axis interpolation;</p>
        <p>L: Linear interpolation;</p>
        <p>C: Circular interpolation,</p>
        <p>SP: Stationary axis interpolation,</p>
        <p>SL: Stationary tool linear interpolation,</p>
        <p>SC: Stationary tool circular interpolation</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Pose/Shift</td>
      <td style="text-align:left">
        <p>Target posture (pose) to move to</p>
        <p>It will be omitted if there is a hidden pose.</p>
        <p>If a shift expression is specified with a + or - sign, (hidden pose +
          shift expression) will be applied as the target posture.</p>
      </td>
      <td style="text-align:left">Pose expression or a signed shift expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Speed</td>
      <td style="text-align:left">
        <p>Moving speed of the tool tip</p>
        <p>A unit (mm/sec, cm/min, sec, %) should be added.</p>
      </td>
      <td style="text-align:left">Arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Accuracy</td>
      <td style="text-align:left">
        <p>Arithmetic expression</p>
        <p>The lower the value, the more accurate. If it is 0, the operation will
          occur discontinuously.</p>
      </td>
      <td style="text-align:left">0~7</td>
    </tr>
    <tr>
      <td style="text-align:left">Tool number</td>
      <td style="text-align:left">The number of the tool to be used when the robot is operating</td>
      <td
      style="text-align:left">0~31</td>
    </tr>
    <tr>
      <td style="text-align:left">Conditional expression</td>
      <td style="text-align:left">
        <p>As soon as the conditional expression is true, the robot operation will
          end, and the designated pose is considered to have been reached.</p>
        <p>The result of the conditional expression can be acquired with the result()
          function.</p>
      </td>
      <td style="text-align:left">True if not 0 False if 0</td>
    </tr>
  </tbody>
</table>

### Example

```python
move L,tg=po[0]+sft[1],spd=800mm/sec,accu=0,tool=1
move P,tg=+Shift(0,0,0,0,-10,0),spd=80%,accu=1,tool=3 until di2  (hidden pose)
if result() then *sensor_on
```

If the \[Record\] button of the teach pendant is pressed, a move statement in hidden pose type will be recorded as the current robot position. The hidden pose value can be checked or edited by placing the cursor on the move statement and pressing the \[Property\] button. 

When the \[Command\] button is pressed and the \[Motion\] group is opened, select the move menu. As a result, a pose-type move statement is recorded.





