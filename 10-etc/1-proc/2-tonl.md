# 10.1.2 tonl

`tonl` statement is the procedure for performing position correction for steps between start and end.

### Description

If you know the coordinate transformation relationship, this procedure is applied when you enter the transformation relationship without calculating a separate coordinate transformation relationship.

```python
R=[x,y,z,rx,ry,rz]
```

![](../../_assets/tonl2.png)

For the rotation matrix, it is applied in the order of Rot_z.Rot_y.Rot_x.

### Syntax

```python
tonl <start/end>,<shift>
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
      <td style="text-align:left">start/end</td>
      <td style="text-align:left">
        online transformation start/end<br>
        <ul>
        <li>on: start</li>
        <li>off: end</li>
        </ul>
      </td>
      <td style="text-align:left">on/off</td>
    </tr>
    <tr>
      <td style="text-align:left">shift</td>
      <td style="text-align:left">
        Amount to shift
      </td>
      <td style="text-align:left">shift expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   global sft
   enet1.recv msg # Receive shift amount via Ethernet
   sft=Shift(msg)
   tonl on,sft
   move L,spd=50mm/s,accu=0,tool=1
   move L,spd=10mm/s,accu=0,tool=1
   move L,spd=50mm/s,accu=0,tool=1
   tonl off
```

![](../../_assets/tonl.png)

