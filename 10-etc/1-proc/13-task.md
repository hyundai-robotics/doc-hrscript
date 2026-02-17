# 10.1.13 `task` Statement

The `task` statement is a procedure used to perform multitasking functions.  
For detailed information about the `task` statement, refer to the link below:  
[${cont_model} Controller Function Manual - Multitasking](https://hrbook-hrc.web.app/#/view/doc-multi-task/en/README)  

### Syntax

```python
task start, sub=<subtask number>, job=<program number>
task wait,  sub=<subtask number>
task sync,  id=<identifier>, no=<number of executions with the same id>
task stop,  sub=<subtask number>
task reset, sub=<subtask number>
```
