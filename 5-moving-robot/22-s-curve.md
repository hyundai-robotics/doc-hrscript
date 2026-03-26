# 5.22 scurve

The S‑curve is a motion‑trajectory planning method that treats the speed changes during the acceleration and deceleration phases of robot motion as a smooth curve.

- **Default method**: At the start and end of acceleration the speed changes abruptly, which can cause mechanical shock (jerk).
- **S‑curve method**: Makes the speed change smoothly, minimizing equipment vibration, extending hardware lifespan, and ensuring stable path accuracy during high‑speed operation.

### Syntax
```python
"scurve on, cnd=<condition number>
"scurve off
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Etc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        Whether the S‑curve function is enabled
      </td>
      <td style="text-align:left">on(enable), off(disable)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        cnd (condition number)
      </td>
      <td style="text-align:left">
        Specifies the number of the S‑curve condition to use
      </td>
      <td style="text-align:left">1~16</td>
    </tr>
  </tbody>
</table>


### 사용 예
```python
     scurve on,cnd=1   # Apply S‑curve condition #1
S1   move P,tg=po1,spd=10%,accu=0,tool=0
     scurve off       # Disable S‑curve
S2   move P,tg=po1,spd=10%,accu=0,tool=0
     end
```

{% hint style="info" %}
For detailed information, see the “[7.5.23 S‑curve condition](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/5-application-parameter/23-scurve-condition/README?cont_model=${cont_model})” section of the ${cont_model} controller operation manual.
{% endhint %}
