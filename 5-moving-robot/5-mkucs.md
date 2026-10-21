# 5.5 `mkucs` - make user coordinate system

### Description

A command that creates a user coordinate system with three poses or one pose.   

- When you create with three poses, it is created with the origin pose, an axis pose, plane pose  according to the specified step order.
- If the step order is not specified, it is created with the origin pose, X-axis pose, and XY plane pose.
- When you create with one pose, it is created with the origin pose and the position/direction is based on the pose value.
- If the calculation is not possible, the job execution is interrupted with an error.
- If a reference frame is specified as the last argument, the user coordinate system is defined on that reference frame. If it is not specified, the user coordinate system is defined based on the base coordinate system. (Supported from V70.06-00)


### Syntax

```python
<result variable> = mkucs(<user coord. system number>,<step order>,<origin pose>,<axis pose>,<plane pose>)
or
<result variable> = mkucs(<user coord. system number>,<step order>,<origin pose>,<axis pose>,<plane pose>,<reference frame>)
or
<result variable> = mkucs(<user coord. system number>,<origin pose>,<axis pose>,<plane pose>)
or
<result variable> = mkucs(<user coord. system number>,<origin pose>)
or
<result variable> = mkucs(<user coord. system number>,<origin pose>,<reference frame>)
```

{% hint style="info" %}
To specify a reference frame together with three poses, the step order must also be specified.<br>
(Example) mkucs(1,"OXY",po1,po2,po3,"robot")
{% endhint %}

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
      <td style="text-align:left">step order</td>
      <td style="text-align:left">
        The order of the three poses below, if not specified, will be "OXY" <br>
        (Example) <br>
        "OXY" : origin pose, X axis pose, XY plane pose <br>
        "OYZ" : origin pose, Y axis pose, YZ plane pose <br>
      </td>
      <td style="text-align:left">string variable</td>
    </tr>
    <tr>
      <td style="text-align:left">origin pose</td>
      <td style="text-align:left">
        pose at the origin
      </td>
      <td style="text-align:left">pose variale</td>
    </tr>
    <tr>
      <td style="text-align:left">axis pose</td>
      <td style="text-align:left">
        pose located on the X, Y, Z-axis
      </td>
      <td style="text-align:left">pose variale</td>
    </tr>
    <tr>
      <td style="text-align:left">plane pose</td>
      <td style="text-align:left">
        Pose located on the XY, YZ, ZX-plane
      </td>
      <td style="text-align:left">pose variale</td>
    </tr>
    <tr>
      <td style="text-align:left">reference frame</td>
      <td style="text-align:left">
        The reference frame on which the position and direction of the user coordinate system are defined. If not specified, "base" is used. (Supported from V70.06-00) <br>
        <ul>
        <li>"base" : The user coordinate system is defined on the base coordinate system. Its position does not change even when the robot or additional axes move.</li>
        <li>"robot" : The user coordinate system is defined on the robot coordinate system. When the traveling axis moves, the absolute position of the user coordinate system moves together with the robot.</li>
        <li>"positioner-n" : The user coordinate system is defined on the positioner coordinate system of positioner group n (1~8). When the positioner moves, the user coordinate system moves together with the positioner. The positioner must be calibrated.</li>
        </ul>
        When "robot" or "positioner-n" is specified, the position of the reference frame is calculated from the additional axis (traveling axis/positioner) values recorded in each pose.
      </td>
      <td style="text-align:left">string</td>
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
- E14614 : Occurs when three poses and a reference frame are specified without a step order. Please specify the step order.
- E14615 : Occurs when the reference frame is not "base", "robot", or "positioner-n" (n: 1~8). Please specify the reference frame again.
- E1287 : Occurs when the reference frame is "positioner" without a positioner group number, or when an unconfigured positioner group is specified. Please check the positioner group number.
- E1288 : Occurs when the positioner specified as the reference frame has not been calibrated. Please perform positioner calibration.


### Example

```python
   var p_origin=Pose(0,0,0,0,0,0,"base")
   var p_xaxis=Pose(100,0,0,0,0,0,"base")
   var p_xyplane_=Pose(100,100,0,0,0,0,"base")
   var uc1 = mkucs(1,p_origin,p_xaxis,p_xyplane)
   var uc2 = mkucs(2,p_origin)
   var uc3 = mkucs(1,"OXY",p_origin,p_xaxis,p_xyplane)
   var uc4 = mkucs(3,"OXY",p_origin,p_xaxis,p_xyplane,"robot")
   var uc5 = mkucs(4,"OXY",p_origin,p_xaxis,p_xyplane,"positioner-1")
   var uc6 = mkucs(5,p_origin,"robot")
   end
```

![](../_assets/mkucs.png)

