# 5.1 姿态

姿态是嵌入在 ${cont_model} 控制器中的对象类型，表示机器人的每个轴或工具尖端的笛卡尔坐标和方向。

姿态通过调用构造函数 `Pose()` 创建。所有函数参数都是位置参数。第一个字符串元素被识别为 `format`，第二个字符串元素被识别为 `config`。其余元素都是数字类型。

### format
多个子元素包括坐标系统，使用分号（;）分隔。每个子元素都是可选的，可以以任何顺序出现。

<table>
  <tr>
    <th>子元素名称</th>
    <th>类型</th>
    <th>描述</th>
  </tr>
  <tr>
    <td>crd</td>
    <td>字符串</td>
    <td>坐标系统.<br>如果省略，则使用关节坐标系统.<br>请参见下表。</td>
  </tr>
  <tr>
    <td>sync(p1,p2)</td>
    <td>p1, p2 : 实数</td>
    <td>传感器同步（1或2个位置值）</td>
  </tr>
  <tr>
    <td>mi(mech#[, ...])</td>
    <td>每个机械编号 : 整数 0~7</td>
    <td>机制配置.<br>（mi代表 mech.info.）<br>如果省略，则包含所有机制。</td>
  </tr>
</table>

格式示例；
```python
"base,mi(0,2)" # 基础坐标，包含机械 0 和 2
"" # 坐标省略（关节），没有传感器同步，机制信息省略（所有机械）
"sync(20.5,-12.0),robot" # 传感器同步（pos.1=20.5, pos.2=-12.0），机器人坐标。
```

{% hint style="info" %}
cfg 元素指定机器人配置。有关更多信息，请参阅 ${cont_model} 机器人控制器操作手册中的 "[2.3.2.2 基础和机器人记录坐标](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/2-operation/3-step/2-step-pose-modify/2-base-robot-crd-sys?cont_model=${cont_model})"。
{% endhint %}



```python
var <pose variable name> = Pose(j1, j2, j3, ...)		# 轴坐标
var <pose variable name> = Pose(x, y, z, rx, ry, rz, j7, j8,..., crd, cfg)		# 基础坐标。
```
参考以下创建姿势的示例，适用于6轴加1额外轴，以及笛卡尔坐标加1额外轴。

```python
var po1 = Pose(10, 90, 0, 0, -30, 0, -1240.8)				# axis coordinate
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, -1240.8, "base", "fl;r2")	# base coord.
var po3 = Pose(-1140.8, "mi(2)")	# joint coord., mech. 2
```

另外，姿势构造函数可以通过单个数组或字符串参数调用。通过此方法，可以将文件或数据转换为姿势，通过远程通信获取并使用。

```python
var <pose variable name> = Pose(array)
var <pose variable name> = Pose(string)
```

参考以下示例。

```python
var arr = [10, 90, 0, 0, -30, 0, -1240.8]
var str = "[1850, 0, 2010.5, 0, -90, 0, -1240.8, \"base\", \"fl;r2\"]"
var po3 = Pose(arr)
var po4 = Pose(str)
```

可以通过以下键访问姿势对象的元素。



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
    <td>轴数量</td>
    <td> </td>
  </tr>
   </tr>
    <tr>
    <td>j1~j32</td>
    <td>实数</td>
<td>8字节实数</td>
<td>轴值</td>
<td>毫米，度</td>
</tr>
</tr>
<tr>
<td>x, y, z</td>
<td>实数</td>
<td>8字节实数</td>
<td>工具在笛卡尔坐标中的位置</td>
<td>毫米</td>
</tr>
</tr>
<tr>
<td>rx, ry, rz</td>
<td>实数</td>
<td>8字节实数</td>
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
<td>基座</td>
<td>基座坐标</td>
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
<td rowspan="7">可以通过<br>用";"分割来进行组合<br><br>默认情况下所有标志均关闭。</td>
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
    <td>auto</td>
    <td>自动 (自动决策)</td>
    <td></td>
  </tr>
  <tr>
    <td>mechinfo</td>
    <td>整数</td>
    <td>-1 ~ 255</td>
    <td>位字段<br>(bit0:M0, bit1:M1, .... bit7:M7)<br>-1表示所有机械。</td>
    <td>仅对应于包含机制的位被设置为1。</td>
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


1. 对于 V60.06-06 或更早版本，`fl` 为 `非翻转`。
姿态元素值可以通过以下示例访问。

```python
po1.j2 = po1.j2 + 5
print po2.z, po2.cfg
```