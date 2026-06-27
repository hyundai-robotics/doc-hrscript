# 4.1.1 数组

数组是一种变量类型，可以在单个名称下收集和存储多个值，并通过索引号访问。

数组被定义为 `var` 或 `global`，与其他变量一样。

{% hint style="warning" %}
[全局变量中顶级数组的名称对大小写不敏感，因此请注意。](../../2-basic-syntax/2-identifier.md)
{% endhint %}


数组的定义和访问格式如下。

|  |  |
| :--- | :--- |
| 定义 | var array name = \[ Value, Value, ...\] |
| 访问 | Array name \[Index\] |

构成数组的值称为 `elements.` 距离，在以下示例中，数组总共有五个元素。索引从0开始。`distances` 的元素0和元素1分别是10和10.5。



使用 \[ \] 操作符读写数组特定元素的值。以下是定义和访问对象的示例。

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var distances = [ 10, 10.5, 12.7, 11.92, 9.5 ]</p>
        <p>distances[1]=20.5</p>
        <p>print distances[0], distances[1]</p>
        <p>end</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">结果</td>
      <td style="text-align:left">
        <p>10</p>
        <p>20.5</p>
      </td>
    </tr>
  </tbody>
</table>



可以通过使用 `len`\(\) 函数获得数组中的元素数量。之前，`len`\(\) 函数被引入为获取字符串长度的函数。如果将数组作为 `len`\( \) 的参数，将返回数组中的元素数量。

<table>
  <thead>
    <tr>
      <th style="text-align:left">函数名称</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">用法示例</th>
      <th style="text-align:left">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">len(<b>a</b>)</td>
      <td style="text-align:left">如果 <b>a</b> 是字符串，则返回字符串的长度。如果 <b>a</b> 是数组，则返回数组中的元素数量</td>
      <td style="text-align:left">
        <p>len(&quot;HELLO&quot;)</p>
        <p>len([20, 30, 80])</p>
      </td>
      <td style="text-align:left">
        <p>5</p>
        <p>3</p>
      </td>
    </tr>
  </tbody>
</table>



`for-next` 语句主要用于对数组的所有元素执行某些处理。

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var i</p>
        <p>var distances = [ 10, 10.5, 12.7, 11.92, 9.5]</p>
        <p>for i=0 to len(distances)-1</p>
        <p>distances[i] = distances[i]+10</p>
        <p>print distances[i]</p>
        <p>next</p>
        <p>end</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">结果</td>
      <td style="text-align:left">
        <p>20</p>
        <p>20.5</p>
        <p>22.7</p>
        <p>21.92</p>
        <p>19.5</p>
      </td>
    </tr>
  </tbody>
</table>



数组中存储的值可以是不同类型的，这并不重要。

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var i</p>
        <p>var arr = [ 10, &quot;abc&quot;, true]</p>
        <p>for i=0 to 2</p>
        <p>print arr[i]</p>
        <p>next</p>
        <p>end</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">结果</td>
      <td style="text-align:left">
        <p>10</p>
        <p>abc</p>
        <p>true</p>
      </td>
    </tr>
  </tbody>
</table>