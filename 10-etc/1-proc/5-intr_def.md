# 10.1.5 `intr_def`

`intr_def` 是一个指定中断条件、观察间隔和发生中断时运行的程序的过程。

### 语法

中断函数是一种程序调用。当机器人在中断观察间隔内工作时，它会在满足预定义的中断条件时调用指定的作业。当被调用的程序运行完成后，它会返回到先前运行程序的位置并继续运行。

![](../../_assets/intr_def_1.png)

### 简要说明

- 仅在中断观察间隔中操作。
- 支持算术表达式作为中断条件表达式。
- 允许在执行中断程序时处理另一个中断（多个中断）。

### 中断被清除的时间点

如果发生以下操作，所有定义的中断会自动清除。

- 执行 'R0: 任务重置' 时
- 程序第一次运行时
- 更改程序计数器（步骤/功能 #）后开始时

### 示例

```python
intr_def <on/off>,no=<interrupt number>,var=<interrupt condition>,val=<condition matching value>,job=<call program number>,[once]
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
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        定义中断或删除已定义的中断<br>
        <ul>
        <li>打开：定义一个新的中断。</li>
        <li>关闭：删除已定义的中断。 （第三个及后续参数将被忽略。）</li>
        </ul>
      </td>
      <td style="text-align:left">打开/关闭</td>
    </tr>
    <tr>
      <td style="text-align:left">中断号码</td>
      <td style="text-align:left">
        要定义或删除的中断号码。<br>
      </td>
      <td style="text-align:left">算式表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">中断条件</td>
      <td style="text-align:left">
        将导致中断的条件表达式。
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">条件匹配值</td>
      <td style="text-align:left">
        生成中断的条件表达式的值。
      </td>
      <td style="text-align:left">算式表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">调用程序号码</td>
      <td style="text-align:left">
        当发生中断时要调用的程序号码。
      </td>
      <td style="text-align:left">算式表达式</td>
    </tr>
    <tr>
      <td style="text-align:left">[一次]</td>
      <td style="text-align:left">
        在中断监视间隔内只处理一个中断，而不处理额外的中断。
      </td>
      <td style="text-align:left">一次</td>
    </tr>
  </tbody>
</table>


### 错误

- E1351 : 在不删除的情况下重新定义已定义的中断号码时发生。 请检查已创建的程序。
### 示例

```python
   intr_def on,no=1,var=di5,val=1,job=24,once # 定义中断
   move P,spd=30%,accu=3,tool=1
   move L,spd=30mm/s,accu=3,tool=1
   ...
   move L,spd=30mm/s,accu=3,tool=1
   move P,spd=30%,accu=3,tool=1
   intr_def off,no=1 # 删除中断
   move P,spd=30%,accu=3,tool=1
   end
```