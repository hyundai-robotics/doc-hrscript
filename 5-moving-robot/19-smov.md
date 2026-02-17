# 5.19 `smov`

### 描述
`smov` 语句是用于定位器同步的程序。  
有关 `smov` 语句的详细描述，请参阅以下链接。  
[${cont_model} 控制器功能手册 - 定位器同步](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/en/README)

<br><br>

### 语法
```python
smov S<站点编号>,<插值模式>,tg=<目标位置>,spd=<速度>,accu=<精度>,tool=<工具编号>
smov S<站点编号>,<插值模式>,tg=<目标位置>,spd=<速度>,accu=<精度>,tool=<工具编号> 直到 <输入信号>
```