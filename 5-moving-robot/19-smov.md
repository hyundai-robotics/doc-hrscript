# 5.19 `smov`

### Description
The `smov` statement is a procedure used for positioner synchronization.  
For a detailed description of the `smov` statement, refer to the link below.  
[${cont_model} Controller Function Manual - Positioner Synchronization](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/en/README?cont_model=${cont_model})

<br><br>

### Syntax
```python
smov S<station number>,<interpolation mode>,tg=<target position>,spd=<speed>,accu=<Accuracy>,tool=<tool number>
smov S<station number>,<interpolation mode>,tg=<target position>,spd=<speed>,accu=<Accuracy>,tool=<tool number> until <input signal>
```