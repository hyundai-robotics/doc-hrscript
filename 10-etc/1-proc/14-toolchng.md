# 10.1.14 toolchng

The `toolchng` statement is a procedure used to change the servo tool assigned to an additional axis.  
For detailed information about the `toolchng` statement, refer to the link below:  
[${cont_model} Robot Controller Function Manual - Servo Tool Change](https://hrbook-hrc.web.app/#/view/doc-svtool-change/en/README)

### Syntax

```python
toolchng on/off, tg=<change target>, di=<connection complete signal>, wait=<waiting time>
```