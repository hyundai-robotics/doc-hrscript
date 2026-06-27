# 6.1.4 `pulse`

`pulse` 语句是脉冲类型信号输出的过程。

### 描述

在 tlag 时间经过后，以 cnt 次作为高电平（On）持续 ton 时间，低电平（Off）持续 toff 时间输出。

### 语法

```python
pulse <Signal>,tlag=<Lag time>,ton=<On time>,toff=<Off time>,cnt=<output count>
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
      <td style="text-align:left">Signal</td>
      <td style="text-align:left">
        以脉冲形式输出的信号名称<br>
        (仅支持 fb.do 信号。)
      </td>
      <td style="text-align:left">输出信号</td>
    </tr>
    <tr>
      <td style="text-align:left">Lag time</td>
      <td style="text-align:left">
        执行过程后直到脉冲信号开始前的等待时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">On time</td>
      <td style="text-align:left">
        输出信号为高电平（On）状态的时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">Off time</td>
      <td style="text-align:left">
        输出信号为低电平（Off）状态的时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">Number of outputs</td>
      <td style="text-align:left">
        重复脉冲周期的次数
        (0 ~ 1000)
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   pulse do10,tlag=0.0,ton=1.5,toff=0.5,cnt=5
   end
```