# 10.1.4 `triggout`

`triggout` 是一个允许您调整信号输出时间点，使其提前输出 (-) 或延迟输出 (+) 的过程。

### 描述

在持续处理命令的 contpath 1 或 2 的间隔中，您可以在命令位置到达目标位置时（准确性 OK）调整信号输出时间点，使其提前输出 (-) 或延迟输出 (+)。

### 语法

```python
triggout <output variable>,val=<output value>,time=<ahead/behind time>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,x=<X-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,y=<Y-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,z=<Z-direction absolute position>
triggout <output variable>,val=<output value>,dist=<ahead/behind distance>,j=<tcp or axis-direction relative distance>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">output variable</td>
      <td style="text-align:left">
        与输出信号对应的变量<br>
        <ul>
        <li>用户输出变量；do, dob, dow, dol, dof</li>
        <li>系统输出变量；so, sob, sow, sol, sof</li>
        </ul>
      </td>
      <td style="text-align:left">输出变量</td>
    </tr>
    <tr>
      <td style="text-align:left">output value</td>
      <td style="text-align:left">
        当为位输出(do, so)时，0 为关闭，非 0 为开启
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">ahead/behind time</td>
      <td style="text-align:left">
        -10.00 ~ 2.00 [s]<br>
        如果为 (-)，则信号在目标位置到达之前输出；如果为 (+)，则在到达之后输出。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">ahead/behind distance</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        如果为 (-)，则信号在目标位置到达之前输出；如果为 (+)，则在到达之后输出。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">x, y, z 方向的绝对位置</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">tcp 或轴向的相对距离<br>
      tcp : 如果 j=0 则<br>
      轴向方向 : 如果 j=1 以上则<br>
      </td>
      <td style="text-align:left">
        tcp : -3000 ~ 3000 [mm], 轴向方向 : -3000 ~ 3000 [mm] 或 [deg]<br>
        如果为 (-)，则信号在相对距离到达之前输出；如果为 (+)，则在到达之后输出。
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   move L,spd=300mm/s,accu=3,tool=1
   triggout do1,val=1,time=-0.5 #在达到步骤前0.5秒打开do1
   triggout do1,val=1,dist=-100.0,j=0 #当tcp到达步骤位置和相对距离-100mm时打开do1
   triggout do1,val=1,dist=-3.0,j=1 #当轴 1 到达步骤位置和相对距离-100mm时打开do1
   triggout do1,val=1,x=-100.0 #当X坐标值达到-100mm时打开do1
   triggout do1,val=1,x=-100.0,y=-100.0 #当X, Y坐标值达到-100mm时打开do1
   move L,spd=30%,accu=2,tool=1
   end
```

{% hint style="warning" %}
* **包含 `triggout` 命令的步骤** 用作参考点，系统检查是否在 **下一个步骤结束之前发出信号**。  
* 如果 **在该时间范围内没有信号输出**，则显示以下警告：  
  **W0241: _"在步骤范围内未输出triggout信号。"_**

{% endhint %}