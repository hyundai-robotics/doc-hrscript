# 5.18 `axisctrl`

### Description
* `axisctrl` 命令指定在执行 `移动 (move)` 命令以移动每个轴时，是否应让额外的轴移动到其目标位置。
* 有关 `axisctrl` 语句的详细描述，请参阅下面的链接。  
[${cont_model} Controller Function Manual - Multitasking](https://hrbook-hrc.web.app/#/view/doc-multi-task/zh/README?cont_model=${cont_model})

### Syntax
```python
axisctrl <on/off>,a=<additional axis number>
axisctrl <on/off>,a=[additional axis number, additional axis number, ...]  # 允许多重指定（最多 4 个）
```