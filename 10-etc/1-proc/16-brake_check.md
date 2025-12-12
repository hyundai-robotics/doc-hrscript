# 10.1.16 brake_check statement

The `brake_check` statement is a procedure that applies torque to each axis motor to diagnose whether the brake is functioning correctly.

### Description

![](../../_assets/brake_check.png)

* **Hold test**  
  With the brake engaged, torque is applied to each axis for 3 seconds and the change in motor angle is checked to see if it is below the threshold.

* **Release test**  
  With the brake released, torque is applied to each axis for 3 seconds and the change in motor angle is checked to see if it is above the threshold.

### Syntax

```python
brake_check  
brake_check os=<error output signal> 
brake_check job=<return program>
brake_check os=<error output signal>,job=<return program>
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
      <td style="text-align:left">Error output signal</td>
      <td style="text-align:left">
         Signal to be output when the angle change exceeds the threshold<br>
         - If specified, a warning occurs and the signal is output.<br>
         - If not specified, an error occurs.
      </td>
      <td style="text-align:left">Variable</td>
    </tr>
    <tr>
      <td style="text-align:left">Return program</td>
      <td style="text-align:left">
        Program number to execute when the angle change exceeds the threshold.
      </td>
      <td style="text-align:left">Variable</td>
    </tr>
  </tbody>
</table>

### Settings
![](../../_assets/brake_check_setting.png)

- **Mode**  
  Set whether to run threshold-setting mode or diagnostic mode.

- **Brake test items**  
  Set whether to perform Hold and Release tests for each axis.

- **Torque ratio (%)**  
  Set how much torque to apply for each axis.

- **Error detection threshold**  
  When running in diagnostic mode, set the threshold angle for error detection for each axis.  
  When running in threshold-setting mode, the values are set automatically.  
  Only editable with engineer-level privileges or higher.

### Error codes
- E1509: Occurs when the brake test is not completed within 6 seconds.
- E1510: Occurs when the brake does not release.
- E1525 ~ E1527: Occur when the return program is missing or its configuration differs.
- E1529: Occurs when the brake test cannot be performed because the robot is moving, running independently, etc.
- E1530: Occurs when execution of the brake test is delayed.
- E21005/W21005: Occur when the angle change during the Hold test is greater than the angle change during the Release test.

### Example

```python
   var v0
   move P,spd=50%,accu=3,tool=1
   brake_check os=do50,job=9000    # On error, output do50 and execute job program number 9000
   end
```

{% hint style="warning" %}
* Do not enter the operating area or touch the robot while the product is operating. There is a risk of injury.
{% endhint %}

{% hint style="info" %}
* Supported only on robots equipped with the gas spring
* For accurate estimation, [Axis add weight setting](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/7-system/4-robot-parameter/7-axis-add-weight/README) and [Load estimation function](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/7-system/7-auto-calibration/3-load-estimation) must be preceded before using the function.
* For a detailed description of the brake check monitoring function, please refer to the link below.
[](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/6-monitoring/4-system/2-system-diagnosis/1-brake-check)
{% endhint %}