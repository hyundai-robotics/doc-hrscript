# 10.1.4 triggout

`triggout` is a procedure that allows you to adjust the signal output time-point to be output-ahead (-) or output-behind (+).

### Description

In the interval of contpath 1, or 2 for continuous processing of commands, you can adjust the signal output time-point when the command position arrives at the target position (Accuracy OK) to be output-ahead (-) or output-behind (+).


### Syntax

```python
triggout <output variable>,val=<output value>,time=<ahead/behind time>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,x=<X-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,y=<Y-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,z=<Z-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,j=<tcp or axis-direction relative distance>
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
      <td style="text-align:left">output variable</td>
      <td style="text-align:left">
        Variable corresponding to output signal<br>
        <ul>
        <li>user output variable; do, dob, dow, dol, dof</li>
        <li>system output variable; so, sob, sow, sol, sof</li>
        </ul>
      </td>
      <td style="text-align:left">output variable</td>
    </tr>
    <tr>
      <td style="text-align:left">output value</td>
      <td style="text-align:left">
        arithmetic expression,<br>
        When it is bit output(do, so), 0 is off, not 0 is on
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">ahead/behind time</td>
      <td style="text-align:left">
        -10.00 ~ 2.00 [s]<br>
        If it is (-), the signal is output before the target position is reached; if it is (+), it is output after it is reached.
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">ahead/behind distance</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        If it is (-), the signal is output before the target position is reached; if it is (+), it is output after it is reached.
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Absolute position in x, y, z direction</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        If it is (-), the signal is output before the target position is reached; if it is (+), it is output after it is reached.
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">tcp or axial relative distance<br>
      tcp : if j=0 then<br>
      axis-direction : if j=1 over then<br>
      </td>
      <td style="text-align:left">
        tcp : -3000 ~ 3000 [mm], axis-direction : -3000 ~ 3000 [mm] or [deg]<br>
        If it is (-), the signal is output before the relative distance is reached; if it is (+), it is output after it is reached.
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   move L,spd=300mm/s,accu=3,tool=1
   triggout do1,val=1,time=-0.5 #turn on do1 0.5 seconds before reaching the step
   triggout do1,val=1,dist=-100.0,j=0 #do1 turns on when tcp reaches step position and relative distance -100mm
   triggout do1,val=1,dist=-3.0,j=1 #do1 turns on when axis 1 reaches step position and relative distance -100mm
   triggout do1,val=1,x=-100.0 #do1 turns on when the X coordinate value reaches -100mm
   triggout do1,val=1,x=-100.0,y=-100.0 #do1 turns on when the X, Y coordinate value reaches -100mm
   move L,spd=30%,accu=2,tool=1
   end
```
