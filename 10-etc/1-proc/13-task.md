# 10.1.13 `任务 (task)` 语句

`任务 (task)` 语句是用于执行多任务功能的过程。  
有关 `任务 (task)` 语句的详细信息，请参阅以下链接：  
[${cont_model} 控制器功能手册 - 多任务处理](https://hrbook-hrc.web.app/#/view/doc-multi-task/zh/README?cont_model=${cont_model})  

### 语法

```python
task start, sub=<subtask number>, job=<program number>
task wait,  sub=<subtask number>
task sync,  id=<identifier>, no=<number of executions with the same id>
task stop,  sub=<subtask number>
task reset, sub=<subtask number>
```