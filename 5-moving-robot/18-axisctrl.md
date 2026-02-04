# 5.18 axisctrl

### Description
* The `axisctrl` command specifies whether additional axes should move to their target positions when the `move` command is executed to move each axis.
* For a detailed description of the `axisctrl` statement, refer to the link below.  
[${cont_model} Controller Function Manual - Multitasking](https://hrbook-hrc.web.app/#/view/doc-multi-task/en/README)

### Syntax
```python
axisctrl <on/off>,a=<additional axis number>
axisctrl <on/off>,a=[additional axis number, additional axis number, ...]  # Multiple specification possible (up to 4)
```