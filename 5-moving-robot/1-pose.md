# 5.1 Pose

Pose is an object type embedded in the ${cont_model} Controller and represents each axis of the robot or the Cartesian coordinates and direction of the tool tip. 

Poses are created by calling the constructor function `Pose()`. All function parameters are position parameters. The first string element is recognized as the `format`, and the second string element as the `config`. The remaining elements are all numeric type.

### format
Multiple sub-elements including the coordinate system are listed, separated by semicolons (;). Each sub-element is optional and can appear in any order.

<table>
  <tr>
    <th>Sub-element name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>crd</td>
    <td>string</td>
    <td>coordinate system.<br>If omitted, joint coordinate system is used.<br>
See table below.</td>
  </tr>
  <tr>
    <td>sync(p1,p2)</td>
    <td>p1, p2 : real</td>
    <td>sensor sync (1 or 2 position values)</td>
  </tr>
  <tr>
    <td>mi(mech#[, ...])</td>
    <td>Each mech number : integer 0~7</td>
    <td>Mechanism configuration.<br>(mi stands for mech.info.)<br>If omitted, all mechanisms are included.</td>
  </tr>
</table>

Examples of format;
```python
"base,mi(0,2)" # Base coord., mech. 0 and 2 included
"" # Coord. omitted (joint), no sensor sync, mechinfo omitted (all mech.)
"sync(20.5,-12.0),robot" # Sensor sync (pos.1=20.5, pos.2=-12.0), robot coord.
```

{% hint style="info" %}
The cfg element specifies the robot configuration. For more information, refer to "[2.3.2.2 Base and Robot Recording Coordinates](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/2-operation/3-step/2-step-pose-modify/2-base-robot-crd-sys)" in the ${cont_model} Robot Controller Operation Manual.
{% endhint %}



```python
var <pose variable name> = Pose(j1, j2, j3, ...)		# axis coordinate
var <pose variable name> = Pose(x, y, z, rx, ry, rz, j7, j8,..., crd, cfg)		# base coord.
```

Refer to the following examples of creating the poses for 6 axes + 1 additional axis and for Cartesian + 1 additional axis.

```python
var po1 = Pose(10, 90, 0, 0, -30, 0, -1240.8)				# axis coordinate
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, -1240.8, "base", "fl;r2")	# base coord.
var po3 = Pose(-1140.8, "mi(2)")	# joint coord., mech. 2
```

Alternatively, the pose constructor function may be called using a single array or string parameter. With this, files or data may be converted into poses, acquired through remote communication, and used.

```python
var <pose variable name> = Pose(array)
var <pose variable name> = Pose(string)
```

Refer to the following example.

```python
var arr = [10, 90, 0, 0, -30, 0, -1240.8]
var str = "[1850, 0, 2010.5, 0, -90, 0, -1240.8, \"base\", \"fl;r2\"]"
var po3 = Pose(arr)
var po4 = Pose(str)
```

Elements of the pose object can be accessed with the following keys.



<!--![](../_assets/image_5.png)-->

<table>
  <tr>
    <th>Key</th>
    <th>Type</th>
    <th>Value range</th>
    <th>Description</th>
    <th>Unit, Remarks</th>
  </tr>
    <tr>
    <td>nj</td>
    <td>Integer</td>
    <td>1~32</td>
    <td>Axis count</td>
    <td> </td>
  </tr>
   </tr>
    <tr>
    <td>j1~j32</td>
    <td>Real</td>
    <td>8-byte real mumber</td>
    <td>Axis value</td>
    <td>mm, deg</td>
  </tr>
   </tr>
    <tr>
    <td>x, y, z</td>
    <td>Real</td>
    <td>8-byte real mumber</td>
    <td>Tool position in Cartesian coordinate</td>
    <td>mm</td>
  </tr>
   </tr>
    <tr>
    <td>rx, ry, rz</td>
    <td>Real</td>
    <td>8-byte real mumber</td>
    <td>Euler angle of tool orientation</td>
    <td>deg</td>
  </tr>
  <tr>
    <td rowspan="4">crd</td>
    <td rowspan="4">String</td>
    <td>joint</td>
    <td>Joint coordinate (default)</td>
    <td rowspan="4"></td>
  </tr>
  <tr>
    <td>base</td>
    <td>Base coordinate</td>
  </tr>
  <tr>
    <td>robot</td>
    <td>Robot coordinate</td>
  </tr>
  <tr>
    <td>u1 ~ u10</td>
    <td>User coordinate</td>
  </tr>
  <tr>
    <td rowspan="8">cfg</td>
    <td rowspan="8">String</td>
    <td>s</td>
    <td>|S|>=180</td>
    <td rowspan="7">Possible to perform<br>combination by <br>dividing with ";"<br><br>The default is all flags turned off.</td>
  </tr>
  <tr>
    <td>r1</td>
    <td>|R1|>=180</td>
  </tr>
  <tr>
    <td>r2</td>
    <td>|R2|>=180</td>
  </tr>
  <tr>
    <td>b</td>
    <td>|B|>=180</td>
  </tr>
  <tr>
    <td>re</td>
    <td>rear</td>
  </tr>
  <tr>
    <td>dn</td>
    <td>down</td>
  </tr>
  <tr>
    <td>nf</td>
    <td>non-flip</td>
  </tr>
  <tr>
    <td>auto</td>
    <td>auto (automatic desision)</td>
    <td></td>
  </tr>
  <tr>
    <td>mechinfo</td>
    <td>Integer</td>
    <td>-1 ~ 255</td>
    <td>bitfield<br>(bit0:M0, bit1:M1, .... bit7:M7)<br>-1 is all mech.</td>
    <td>Only the bits corresponding to the included mechanisms are set to 1.</td>
  </tr>
  <tr>
    <td>nsync</td>
    <td>Integer</td>
    <td>0~2</td>
    <td>The number of sensor-sync</td>
    <td></td>
  </tr>
  <tr>
    <td>sync</td>
    <td>String (p1, p2; integer)</td>
    <td>sync(p1,p2)</td>
    <td>Sensor-sync values</td>
    <td>sync(220.5,195.3)</td>
  </tr>
</table>


1. For V60.06-06 or older versions, fl is non-fl.

The pose element values can be accessed as shown in the following example.

```python
po1.j2 = po1.j2 + 5
print po2.z, po2.cfg
```



