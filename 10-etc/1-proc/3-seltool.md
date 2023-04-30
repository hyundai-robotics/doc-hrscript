# 10.1.3 seltool

`seltool` is a procedure to change the tool number.

### Description

The tool is divided into a robot tool attached to the robot flange and a station tool installed separately from the robot, and `seltool` changes the tool number of each type.


### Syntax

```python
seltool <tool number>,<tool type>
```

### Parameters

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
      <td style="text-align:left">tool number</td>
      <td style="text-align:left">
        tool number<br>
        <ul>
        <li>robot tool: 0 ~ 31</li>
        <li>station tool: 0 ~ 3</li>
        </ul>
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">tool type</td>
      <td style="text-align:left">
        tool type to change tool number<br>
        <ul>
        <li>robot tool: robot</li>
        <li>station tool: station</li>
        </ul>
      </td>
      <td style="text-align:left">robot/station</td>
    </tr>
  </tbody>
</table>

### Sample

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
