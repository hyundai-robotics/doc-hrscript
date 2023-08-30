# 5.5 mkucs - make user coordinate system

### Description

A command that creates a user coordinate system with three poses or one pose.   

- When you create with three poses, it is created with an origin pose, an X-axis pose, and an XY-plane pose.
- When you create with one pose, it is created with the origin pose and the position/direction is based on the pose value.
- If the calculation is not possible, the job execution is interrupted with an error.


### Syntax

```python
<result variable> = mkucs(<user coord. system number>,<origin pose>,<X-axis pose>,<XY-plane pose>)
or
<result variable> = mkucs(<user coord. system number>,<origin pose>)
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
      <td style="text-align:left">result variable</td>
      <td style="text-align:left">
        result of background execution<br>
        <ul>
        <li>0: Successfully completed.</li>
        <li>-1: Failed to create user coord. system.</li>
        </ul>
      </td>
      <td style="text-align:left">Variable</td>
    </tr>
    <tr>
      <td style="text-align:left">user coord. system number</td>
      <td style="text-align:left">
        umber of the user coordinate system to create
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">origin pose</td>
      <td style="text-align:left">
        pose at the origin
      </td>
      <td style="text-align:left">pose variale</td>
    </tr>
    <tr>
      <td style="text-align:left">X-axis pose</td>
      <td style="text-align:left">
        pose located on the X-axis
      </td>
      <td style="text-align:left">pose variale</td>
    </tr>
    <tr>
      <td style="text-align:left">XY-plane pose</td>
      <td style="text-align:left">
        Pose located on the XY-plane
      </td>
      <td style="text-align:left">pose variale</td>
    </tr>
  </tbody>
</table>

### Return value


<table>
  <thead>
    <tr>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Etc.</th>
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


### Errors

- E14613 : Occurs when the actual parameter does not match the formal parameter. Check the actual parameters.
- E14614 : Occurs when the user coordinate number is not a number. Please specify the user coordinate number again.
- E14615 : Occurs when the user coordinate number is not a number between 1 and 20. Please change the user coordinate number.
- E1011 : Occurs when the distance between the taught poses is too close. Occurs when the distance between each point is less than 1mm. Please correct the distance value between poses.
- E1012 : Occurs when three called poses are in a straight line.


### Example

```python
   var p_origin=Pose(0,0,0,0,0,0,"base")
   var p_xaxis=Pose(100,0,0,0,0,0,"base")
   var p_xyplane_=Pose(100,100,0,0,0,0,"base")
   var uc1 = mkucs(1,p_origin,p_xaxis,p_xyplane)
   var uc2 = mkucs(2,p_origin)
   end
```

![](../../_assets/mkucs.png)

