# 6.1.2 示例

请参阅以下用法示例。

```python
do2=1		# 打开 fb0 的编号 0 的位输出值
fb2.dob3=0b00001111  	# 将 fb2 的第 3 个字节输出值指定为二进制位字符串
fb[4].dob1=0x0F  	# 打开 fb4 的第 1 个字节输出值的低 4 位，并关闭高 4 位
var work_no=fb9.dib3    # 将 fb9 的第 3 个字节输入值分配给 work_no 变量
if fb5.di43 then *err  	# 当 fb5.di42 被打开时分支到 *err 标签
for idx=21 to 29
  fb3.do[idx]=1  	# 打开 fb3 的所有输出信号 do21 ~ do29 
next
fb2.do3=fb2.do7=fb2.do11=1   # 同时打开 fb2 的第 3、第 7 和第 11 个输出信号
```