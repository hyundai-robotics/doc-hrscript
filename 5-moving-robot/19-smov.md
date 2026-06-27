# 5.19 `smov`

### 描述
`smov` 语句是用于定位器同步的程序。  
有关 `smov` 语句的详细描述，请参见以下链接。  
[${cont_model} 控制器功能手册 - 定位器同步](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/zh/README?cont_model=${cont_model})

<br><br>

### 语法
```python
smov S<station number>,<interpolation mode>,tg=<target position>,spd=<speed>,accu=<Accuracy>,tool=<tool number>
smov S<station number>,<interpolation mode>,tg=<target position>,spd=<speed>,accu=<Accuracy>,tool=<tool number> until <input signal>
```