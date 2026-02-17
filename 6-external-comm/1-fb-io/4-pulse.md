# 6.1.4 `pulse`

`pulse`语句是脉冲类型信号输出的过程。

### 描述

在延迟时间经过后，它以On(高)状态输出cnt次，持续ton时间，然后以Off(低)状态持续toff时间。

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
      <td style="text-align:left">信号</td>
      <td style="text-align:left">
        要以脉冲形式输出的信号名称<br>
        (仅支持fb.do信号。)
      </td>
      <td style="text-align:left">输出信号</td>
    </tr>
    <tr>
      <td style="text-align:left">延迟时间</td>
      <td style="text-align:left">
        执行该过程后，脉冲信号开始前的等待时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">开启时间</td>
      <td style="text-align:left">
        输出信号在On(高)状态下的持续时间<br>
        (0.0 ~ 100.0[秒])
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
<tr>
      <td style="text-align:left">关闭时间</td>
      <td style="text-align:left">
        关闭（低）状态时输出信号的时间<br>
        （0.0 ~ 100.0[秒]）
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">输出次数</td>
      <td style="text-align:left">
        重复脉冲周期的次数
        （0 ~ 1000）
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