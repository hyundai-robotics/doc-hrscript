# 10.1.16 `brake_check`

`brake_check`语句是一个程序，通过对每个轴电机施加扭矩来诊断制动器是否正常工作。

### 描述

![](../../_assets/brake_check.png)

* **保持测试**  
  在制动器保持锁定的情况下，对每个轴施加3秒的扭矩，并检查电机角度的变化是否低于阈值。

* **释放测试**  
  在制动器释放的情况下，对每个轴施加3秒的扭矩，并检查电机角度的变化是否高于阈值。

### 语法

```python
brake_check  
brake_check os=<error output signal> 
brake_check job=<return program>
brake_check os=<error output signal>,job=<return program>
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
      <td style="text-align:left">错误输出信号</td>
      <td style="text-align:left">
         当角度变化超过阈值时输出的信号<br>
         - 如果指定，将触发警告并输出信号。<br>
         - 如果未指定，将发生错误。
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">返回程序</td>
      <td style="text-align:left">
        当角度变化超过阈值时要执行的程序号。
      </td>
      <td style="text-align:left">变量</td>
    </tr>
</tbody>
</table>

### 设置
当您在 brake_check 命令中触摸 [属性] 按钮时，将进入刹车诊断设置屏幕。  
![](../../_assets/brake_check_setting.png)

- **模式**  
  设置是运行阈值设置模式还是诊断模式。

- **刹车测试项目**  
  设置是否对每个轴执行保持和释放测试。

- **扭矩比 (%)**  
  设置每个轴施加多少扭矩。

- **错误检测阈值**  
  在诊断模式下运行时，设置每个轴的错误检测阈值角度。  
  在阈值设置模式下，值会自动设置。  
  仅可由工程师级别或更高权限编辑。

### 错误代码
- E1509：当刹车测试在 6 秒内未完成时发生。
- E1510：当刹车未释放时发生。
- E1525 ~ E1527：当返回程序缺失或其配置不同时发生。
- E1529：当机器人正在移动、独立运行等时，无法执行刹车测试。
- E1530：当刹车测试执行延迟时发生。
- E21005/W21005：当保持测试期间的角度变化大于释放测试期间的角度变化时发生。

### 示例

```python
   var v0
   move P,spd=50%,accu=3,tool=1
   brake_check os=do50,job=9000    # 在错误时，输出 do50 并执行作业程序编号 9000
   end
```

{% hint style="warning" %}
* 在产品操作时，请勿进入操作区域或触摸机器人。存在受伤风险。
{% endhint %}

{% hint style="info" %}
* 仅支持配备气弹簧的机器人
* 为了准确估计，必须在使用该功能之前进行 [轴添加重量设置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/4-robot-parameter/7-axis-add-weight/README?cont_model=${cont_model}) 和 [负载估计功能](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/7-auto-calibration/3-load-estimation?cont_model=${cont_model})。
* 有关刹车检查监控功能的详细说明，请参阅以下链接。
[](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/4-system/2-system-diagnosis/1-brake-check?cont_model=${cont_model})
{% endhint %}