# _weaving

### Description

_weaving is used to change the currently selected weaving conditions.

### Syntax

```python
_weaving.frequency=2
_weaving.angle=5
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">item</th>
      <th style="text-align:left">meanings</th>
      <th style="text-align:left">etc</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">weave</td>
      <td style="text-align:left">
         Weaving type (0=single vibration, 1=triangle, 2=L-shaped, 3=circular)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">frequency</td>
      <td style="text-align:left">
        Frequency[Hz]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">left_distance</td>
      <td style="text-align:left">
        Distance towards left[mm]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">right_distance</td>
      <td style="text-align:left">
        Distance towards right[mm]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">angle</td>
      <td style="text-align:left">
        Angle[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">offset_angle</td>
      <td style="text-align:left">
        Offset angle[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">wall_direction</td>
      <td style="text-align:left">
        Wall direction (0=vertical, 1=horizontal, 2=torch orientation)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">forward_angle</td>
      <td style="text-align:left">
        Forward angle[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">boundary_limit</td>
      <td style="text-align:left">
        Boundary limit (0=valid, 1=invalid)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_time_1</td>
      <td style="text-align:left">
        Segment (1~4) moving time[s]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_delay_1</td>
      <td style="text-align:left">
        Segment (1~4) timer(weaving stop)[s]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_mode</td>
      <td style="text-align:left">
        Height sensing mode (0=current change, 1=left fixed, 2=right fixed)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_mode</td>
      <td style="text-align:left">
        Left/Right sensing mode (0=Center, 1=Left, 2=Right)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">asymetric_sensing_ratio</td>
      <td style="text-align:left">
        Asymmetric sensing ratio (-50~50) [%]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_sensitivity</td>
      <td style="text-align:left">
        Left and right sensing sensitivity (0~10)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_sensitivity</td>
      <td style="text-align:left">
        Height sensing sensitivity (0~10)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
  </tbody>
</table>




### Sample

```python
   weaving on,cnd=1
   move P,spd=50%,accu=3,tool=1
   _weaving.frequency=5    # Change the weaving frequency to 5Hz
   move P,spd=50%,accu=3,tool=1
   weaving off
   end
```

