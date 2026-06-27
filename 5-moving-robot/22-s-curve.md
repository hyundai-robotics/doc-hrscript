# 5.22 scurve

S-曲线是一种运动轨迹规划方法，在机器人运动的加速和减速阶段，将速度变化视为平滑曲线。

- **默认方法**：在加速的开始和结束时，速度变化突然，这可能会导致机械冲击（冲击力）。
- **S-曲线方法**：使速度变化平滑，从而最小化设备振动，延长硬件寿命，并确保在高速操作期间路径的稳定准确性。

### 语法
```python
"scurve on, cnd=<condition number>
"scurve off
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">项目</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        S-曲线功能是否启用
      </td>
      <td style="text-align:left">on(启用), off(禁用)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        cnd (条件编号)
      </td>
      <td style="text-align:left">
        指定要使用的S-曲线条件的编号
      </td>
      <td style="text-align:left">1~16</td>
    </tr>
  </tbody>
</table>


### 使用示例
```python
     scurve on,cnd=1   # 应用S-曲线条件#1
S1   move P,tg=po1,spd=10%,accu=0,tool=0
     scurve off       # 禁用S-曲线
S2   move P,tg=po1,spd=10%,accu=0,tool=0
     end
```

{% hint style="info" %}
有关详细信息，请参见${cont_model}控制器操作手册的"[7.5.23 S-曲线条件](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/5-application-parameter/23-scurve-condition/README?cont_model=${cont_model})"部分。
{% endhint %}