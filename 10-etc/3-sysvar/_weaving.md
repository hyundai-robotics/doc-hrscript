# `_weaving`

### Description

`_weaving` 用于更改当前选择的编织条件。

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
         编织类型 (0=单振动, 1=三角形, 2=L形, 3=圆形)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">frequency</td>
      <td style="text-align:left">
        频率[Hz]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">left_distance</td>
      <td style="text-align:left">
        向左的距离[mm]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">right_distance</td>
      <td style="text-align:left">
        向右的距离[mm]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">angle</td>
      <td style="text-align:left">
        角度[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">offset_angle</td>
      <td style="text-align:left">
        偏移角度[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">wall_direction</td>
      <td style="text-align:left">
        墙面方向 (0=垂直, 1=水平, 2= torch 方向)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">forward_angle</td>
      <td style="text-align:left">
        向前角度[deg]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">boundary_limit</td>
      <td style="text-align:left">
        边界限制 (0=有效, 1=无效)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_time_1</td>
      <td style="text-align:left">
        段 (1~4) 移动时间[s]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_delay_1</td>
      <td style="text-align:left">
        段 (1~4) 计时器(编织停止)[s]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_mode</td>
      <td style="text-align:left">
        高度感应模式 (0=当前变化, 1=左固定, 2=右固定)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_mode</td>
      <td style="text-align:left">
        左/右感应模式 (0=中心, 1=左, 2=右)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">asymetric_sensing_ratio</td>
      <td style="text-align:left">
        非对称感应比例 (-50~50) [%]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_sensitivity</td>
      <td style="text-align:left">
        左右感应灵敏度 (0~10)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_sensitivity</td>
      <td style="text-align:left">
        高度感应灵敏度 (0~10)
      </td>
      <td style="text-align:left">variable</td>
    </tr>
  </tbody>
</table>




### Sample

```python
   weaving on,cnd=1
   move P,spd=50%,accu=3,tool=1
   _weaving.frequency=5    # 将编织频率改为5Hz
   move P,spd=50%,accu=3,tool=1
   weaving off
   end
```