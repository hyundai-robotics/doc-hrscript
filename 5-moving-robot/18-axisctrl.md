# 5.18 `axisctrl`

### 描述
* `axisctrl` 命令指定在执行 `移动 (move)` 命令以移动每个轴时，是否应当额外轴移动到其目标位置。
* 有关 `axisctrl` 声明的详细描述，请参阅以下链接。  
[${cont_model} 控制器功能手册 - 多任务处理](https://hrbook-hrc.web.app/#/view/doc-multi-task/zh/README?cont_model=${cont_model})

### 语法
```python
axisctrl <on/off>,a=<additional axis number>
axisctrl <on/off>,a=[additional axis number, additional axis number, ...]  # 多重指定可能（最多 4 个）
```