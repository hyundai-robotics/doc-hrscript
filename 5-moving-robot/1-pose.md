# 5.1 位姿

位姿是嵌入在 ${cont_model} 控制器中的对象类型，表示机器人每个轴或工具尖端的笛卡尔坐标和方向。

通过调用构造函数 `Pose()` 来创建位姿。所有函数参数都是位置参数。第一个字符串元素被识别为 `format`，第二个字符串元素为 `config`。其余元素均为数值类型。

### format
多个子元素，包括坐标系，用分号 (;) 分隔列出。每个子元素都是可选的，可以按任何顺序出现。

<table>
  <tr>
    <th>子元素名称</th>
    <th>类型</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>crd</td>
    <td>字符串</td>
    <td>坐标系。<br>如果省略，则使用关节坐标系。<br>请参见下表。</td>
  </tr>
  <tr>
    <td>sync(p1,p2)</td>
    <td>p1, p2 : 实数</td>
    <td>传感器同步 (1 或 2 个位置值)</td>
  </tr>
  <tr>
    <td>mi(mech#[, ...])</td>
    <td>每个机械数字 : 整数 0~7</td>
    <td>机械配置。<br>(mi 代表 mech.info.)<br>如果省略，则包含所有机械。</td>
  </tr>
</table>

格式示例；
```python
"base,mi(0,2)" # 基坐标，包含机械 0 和 2
"" # 坐标省略（关节），无传感器同步，机械信息省略（所有机械）
"sync(20.5,-12.0),robot" # 传感器同步（pos.1=20.5, pos.2=-12.0），机器人坐标
```

{% hint style="info" %}
cfg 元素指定机器人配置。有关更多信息，请参阅 ${cont_model} 控制器操作手册中的 "[2.3.2.2 基础和机器人记录坐标](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/2-operation/3-step/2-step-pose-modify/2-base-robot-crd-sys?cont_model=${cont_model})"。
{% endhint %}

```python
var <pose 变量名称> = Pose(j1, j2, j3, ...)		# 轴坐标
var <pose 变量名称> = Pose(x, y, z, rx, ry, rz, j7, j8,..., crd, cfg)		# 基坐标
```

请参考以下创建 6 轴 + 1 个附加轴和笛卡尔 + 1 个附加轴的位姿示例。

```python
var po1 = Pose(10, 90, 0, 0, -30, 0, -1240.8)				# 轴坐标
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, -1240.8, "base", "fl;r2")	# 基坐标
var po3 = Pose(-1140.8, "mi(2)")	# 关节坐标，机械 2
```

或者，可以使用单个数组或字符串参数调用位姿构造函数。通过这种方式，可以将文件或数据转换为位姿，通过远程通信获取并使用。

```python
var <pose 变量名称> = Pose(array)
var <pose 变量名称> = Pose(string)
```

请参考以下示例。

```python
var arr = [10, 90, 0, 0, -30, 0, -1240.8]
var str = "[1850, 0, 2010.5, 0, -90, 0, -1240.8, \"base\", \"fl;r2\"]"
var po3 = Pose(arr)
var po4 = Pose(str)
```

位姿对象的元素可以使用以下键访问。



<!--![](../_assets/image_5.png)-->

<table>
  <tr>
    <th>键</th>
    <th>类型</th>
    <th>值范围</th>
    <th>描述</th>
    <th>单位，备注</th>
  </tr>
    <tr>
    <td>nj</td>
    <td>整数</td>
    <td>1~32</td>
    <td>轴数</td>
    <td> </td>
  </tr>
   </tr>
    <tr>
    <td>j1~j32</td>
    <td>实数</td>
    <td>8 字节实数</td>
    <td>轴值</td>
    <td>毫米，度</td>
  </tr>
   </tr>
    <tr>
    <td>x, y, z</td>
    <td>实数</td>
    <td>8 字节实数</td>
    <td>工具在笛卡尔坐标中的位置</td>
    <td>毫米</td>
  </tr>
   </tr>
    <tr>
    <td>rx, ry, rz</td>
    <td>实数</td>
    <td>8 字节实数</td>
    <td>工具方向的欧拉角</td>
    <td>度</td>
  </tr>
  <tr>
    <td rowspan="4">crd</td>
    <td rowspan="4">字符串</td>
    <td>关节</td>
    <td>关节坐标（默认）</td>
    <td rowspan="4"></td>
  </tr>
  <tr>
    <td>基</td>
    <td>基坐标</td>
  </tr>
  <tr>
    <td>机器人</td>
    <td>机器人坐标</td>
  </tr>
  <tr>
    <td>u1 ~ u10</td>
    <td>用户坐标</td>
  </tr>
  <tr>
    <td rowspan="8">cfg</td>
    <td rowspan="8">字符串</td>
    <td>s</td>
    <td>|S|>=180</td>
    <td rowspan="7">可以通过用“;”分隔进行组合。</td>
  </tr>
  <tr>
    <td>r1</td>
    <td>|R1|>=180</td>
  </tr>
  <tr>
    <td>r2</td>
    <td>|R2|>=180</td>
  </tr>
  <tr>
    <td>b</td>
    <td>|B|>=180</td>
  </tr>
  <tr>
    <td>re</td>
    <td>后</td>
  </tr>
  <tr>
    <td>dn</td>
    <td>下</td>
  </tr>
  <tr>
    <td>nf</td>
    <td>非翻转</td>
  </tr>
  <tr>
    <td>自动</td>
    <td>自动（自动决策）</td>
    <td></td>
  </tr>
  <tr>
    <td>mechinfo</td>
    <td>整数</td>
    <td>-1 ~ 255</td>
    <td>位字段<br>(bit0:M0, bit1:M1, .... bit7:M7)<br>-1表示所有机械。</td>
    <td>仅设置与包含的机械对应的位为 1。</td>
  </tr>
  <tr>
    <td>nsync</td>
    <td>整数</td>
    <td>0~2</td>
    <td>传感器同步的数量</td>
    <td></td>
  </tr>
  <tr>
    <td>sync</td>
    <td>字符串 (p1, p2; 整数)</td>
    <td>sync(p1,p2)</td>
    <td>传感器同步值</td>
    <td>sync(220.5,195.3)</td>
  </tr>
</table>

1. 对于 V60.06-06 或更早版本，`fl` 是 `non-fl`。

位姿元素值可以如下示例所示进行访问。

```python
po1.j2 = po1.j2 + 5
print po2.z, po2.cfg
```