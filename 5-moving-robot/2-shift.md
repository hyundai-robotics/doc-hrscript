# 5.2 移动

移动是嵌入在 ${cont_model} 控制器中的对象类型，表示姿态的变化值。

通过调用构造函数 `Shift()` 创建移动。所有函数参数均为位置参数。同时，`crd` 和 `cfg` 为字符串类型，其他为数字类型。

```python
var <shift variable name> = Shift(j1, j2, j3, ...)				# 轴坐标
var <shift variable name> = Shift(x, y, z, rx, ry, rz, j7, j8,..., crd)		# 基座坐标
```

请参阅以下创建 6 轴 + 1 额外轴和笛卡尔 + 1 额外轴的移动示例。

```python
var sft1 = Shift(30, 0, 0, 0, -5.8, 0, -120)				# 轴坐标
var sft2 = Shift(0, 0, 55.2, 0, -5, 0, -120, "base")			# 基座坐标
```

另外，构造函数 shift 也可以通过单个数组或字符串参数调用。通过此方法，可以将文件或数据转换为移动，通过远程通信获取并使用。

```python
var <shift variable name> = Shift(array)
var <shift variable name> = Shift(string)
```

请参考以下示例。

```python
var arr = [30, 0, 0, 0, -5.8, 0, -120]
var str = "[0, 0, 55.2, 0, -5, 0, -120, \"base\"]"
var sft3 = Shift(arr)
var sft4 = Shift(str)
```

可以通过以下键访问移动对象的元素。

![](../_assets/image_7.png)