# 10.2.2 segment

`segment` is the function that divides the distance between the start and end positions evenly.


### Description

Divides the distance between the start and end positions of the function factors evenly and stores the pose value considering the position and posture corresponding to the specified counter in the pose variable.
![](../../_assets/image_segment_1.png)

For example, if P3=segment(P1,P2,3,2), divide the distance between the P2 target positions from the P1 start position into 3 equal parts and store the pose value of the position and rotation of the 2nd pose in the P3 pose variable.

When you add the via position as a paramter of the function, the distance on the arc consisting of the start position, the via point, and the target position is evenly divided and the pose value of the position and rotation is stored in the pose variable.

![](../../_assets/image_segment_2.png)

For example, if P10=segment (P1,P2,P3,4,2),
The distance on the arc consisting of the P1 starting pose and P2 via pose P3 target pose is divided into 4 equal parts, and the pose value of the position and rotation of the specified 2nd pose is stored in the P10 pose variable.

<br>

### Syntax

```python
result=segment(<start pose>,<end pose>,<division number>,<counter>)
```

```python
result=segment(<start pose>,<via pose>,<end pose>,<division number>,<counter>)
```

### Return value

The result pose.

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
      <td style="text-align:left">start pose</td>
      <td style="text-align:left">
        start pose
      </td>
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">via pose</td>
      <td style="text-align:left">
        via pose
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">end pose</td>
      <td style="text-align:left">
        end pose
      </td>
      <td style="text-align:left">pose expression</td>
    </tr>
    <tr>
      <td style="text-align:left">division number</td>
      <td style="text-align:left">
        division number<br>
        (1 ~ 30000)
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">counter</td>
      <td style="text-align:left">
        counter number of the pose to store<br>
        (0 ~ 300000, 0: start pose)
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var po1,po2,po3
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # start pose
     po2=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # end pose
     po3=segment(po1,po2,4,2)
     end
```

```python
     var po1,po2,po3,po10
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # start pose
     po2=Pose(1500.000,500.000,1938.000,0.000,0.000,0.000) # via pose
     po3=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # end pose
     po10=segment(po1,po2,po3,5,3)
     end
```