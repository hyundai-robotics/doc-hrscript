# 10.1.7 gasp_check

The gasp_check statement estimates the pressure of the gas spring mounted on the robot and checks whether it is normal.

### Description

![](../../_assets/gasp_check.png)

- To estimate the pressure, the axis equipped with the gas spring is reciprocated by -20 degrees from its current position.
- You can monitor pressure by saving the estimated pressure as a variable.
- User can enter normal pressure and tolerance. If the estimated pressure exceeds the range, the set error output signal turns on.

### Syntax

```python
gasp_check pres=<estimated pressure>,ref=<normal pressure>,tol=<tolerance>
gasp_check pres=<estimated pressure>,ref=<normal pressure>,tol=<tolerance>,os=<error output signal>
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
      <td style="text-align:left">estimated pressure</td>
      <td style="text-align:left">
         Variables in which the estimated gas spring pressure is stored[bar]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">normal pressure</td>
      <td style="text-align:left">
        Normal pressure to be the reference value for error occurrence[bar]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">tolerance</td>
      <td style="text-align:left">
        estimated pressure error tolerance[bar]
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">error output signal</td>
      <td style="text-align:left">
        Signal output when an error occurs
      </td>
      <td style="text-align:left">output signal variable</td>
    </tr>
  </tbody>
</table>

### Errors
- E21011 : Occurs when the estimated gas spring pressure is below the minimum error criterion.
- E21012 : Occurs when the estimated gas spring pressure is higher than the maximum error reference.
- E21013 : Occurs on robots that do not support gas spring pressure inspection.


### Sample

```python
   var v0
   move P,spd=50%,accu=3,tool=1
   gasp_check pres=v0,ref=120,tol=20,os=do50    # Normal if the estimated pressure is 100 to 140 bar
   end
```

{% hint style="info" %}
* Supported only on robots equipped with the gas spring
* For accurate estimation, [Axis add weight setting](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/7-system/4-robot-parameter/7-axis-add-weight/README) and [Load estimation function](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/7-system/7-auto-calibration/3-load-estimation) must be preceded before using the function.

{% endhint %}

