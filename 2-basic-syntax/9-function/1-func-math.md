# 2.9.1 数学函数

<table style="text-align:left">
  <thead>
    <tr>
      <th>函数</th>
      <th>描述</th>
      <th>用法示例</th>
      <th>结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>abs(<b>a</b>)</td>
      <td>返回 <b>a</b> 的绝对值
      </td>
      <td>abs(-300)</td>
      <td>300</td>
    </tr>
    <tr>
      <td>acos(<b>a</b>)</td>
      <td>返回 <b>a</b> 的反余弦值，单位为弧度</td>
      <td>acos(0.5)</td>
      <td>1.0472</td>
    </tr>
    <tr>
      <td>asin(<b>a</b>)</td>
      <td>返回 <b>a</b> 的反正弦值，单位为弧度</td>
      <td>asin(0.5)</td>
      <td>0.5236</td>
    </tr>
    <tr>
      <td>atan(<b>a</b>)</td>
      <td>返回 <b>a</b> 的反正切值，单位为弧度</td>
      <td>atan(0.5)</td>
      <td>0.4636</td>
    </tr>
    <tr>
      <td>atan2(<b>a</b>, <b>b</b>)</td>
      <td>返回以 <b>a</b> 为 y 值，<b>b</b> 为 x 值的三角形的反正切值，单位为弧度</td>
      <td>atan2(2,1)</td>
      <td>1.1071</td>
    </tr>
		<tr>
			<td>ceil(x)</td>
			<td>返回 <b>x</b> 的向上舍入值。</td>
			<td>
				ceil(3.1415)<br>
				ceil(-3.1415)
			</td>
				<td>
				4<br>
				-3
				</td>
		</tr>
    <tr>
      <td>cos(<b>r</b>)</td>
      <td>返回 <b>r</b> 的余弦值，单位为弧度</td>
      <td>cos(3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>deg2rad(<b>d</b>)</td>
      <td>返回 <b>d</b> 的弧度值，单位为度</td>
      <td>deg2rad(-90)</td>
      <td>-1.570796</td>
    </tr>
    <tr>
      <td>dist(<b>x</b>, <b>y</b>)</td>
      <td>返回从原点到 (<b>x</b>, <b>y</b>) 坐标的欧几里德距离</td>
      <td>dist(3.5,10)</td>
      <td>10.59481</td>
    </tr>
		<tr>
			<td>floor(x)</td>
			<td>返回 <b>x</b> 的向下舍入值。</td>
			<td>
				floor(3.1415)<br>
				floor(-3.1415)
			</td>
			<td>
				3<br>
				-4
			</td>
		</tr>
    <tr>
      <td>max(<b>a</b>, <b>b</b>)</td>
      <td>返回 <b>a</b> 和 <b>b</b> 之间的较大值
      </td>
      <td>max(-1.23, -3)</td>
      <td>-1.23</td>
    </tr>
    <tr>
      <td>min(<b>a</b>, <b>b</b>)</td>
      <td>返回 <b>a</b> 和 <b>b</b> 之间的较小值
      </td>
      <td>max(-1.23, -3)</td>
      <td>-3</td>
    </tr>
    <tr>
      <td>near(<b>a</b>, <b>b</b> [,<b>e</b>])</td>
      <td>如果 <b>a</b> 和 <b>b</b> 之间的实数值的差小于或等于 <b>e</b>，则返回 1；如果差大于 <b>e</b>，则返回 0
      </td>
      <td>
        <p>near(0.005, 0.0058)</p>
        <p>near(0.005, 0.006)</p>
        <p>near(0.005, 0.006, 0.1)</p>
      </td>
      <td>
        <p>1</p>
        <p>0</p>
        <p>1</p>
      </td>
    </tr>
    <tr>
      <td>rad2deg(<b>r</b>)</td>
      <td>返回 <b>r</b> 的度值，单位为弧度</td>
      <td>rad2deg(1.570796)</td>
      <td>90</td>
    </tr>
		<tr>
			<td>round(x)</td>
			<td>返回 <b>x</b> 的四舍五入值。</td>
			<td>
				round(3.1415)<br>
				round(3.7415)<br>
				round(-3.1415)<br>
				round(-3.7415)
			</td>
				<td>
				3<br>
				4<br>
				-3<br>
				-4
				</td>
		</tr>
    <tr>
      <td>sin(<b>r</b>)</td>
      <td>返回 <b>r</b> 的正弦值，单位为弧度</td>
      <td>sin(1.5*3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>sqr(<b>a</b>)</td>
      <td>返回 <b>a</b> 的平方根
      </td>
      <td>
        <p>sqr(16)</p>
        <p>sqr(0)</p>
      </td>
      <td>
        <p>4</p>
        <p>0</p>
      </td>
    </tr>
    <tr>
      <td>tan(<b>r</b>)</td>
      <td>返回 <b>r</b> 的正切值，单位为弧度</td>
      <td>tan(3.141592/4)</td>
      <td>0.9999</td>
    </tr>
		<tr>
			<td>trunc(x)</td>
			<td>返回 <b>x</b> 的截断整数部分。</td>
			<td>
				trunc(3.1415)<br>
				trunc(-3.1415)
			</td>
			<td>
				3<br>
				-3
			</td>
		</tr>
		<tr>
			<td>val_as(format, v)</td>
			<td>
      返回由格式重新解释的 v 值的二进制数据。<br>
			有关支持的格式，请参阅下面的 [Table 1]。
			</td>
			<td>
				val_as("u1", -127)<br>
				val_as("u2", -2)<br>
				val_as("s4", -2147483648)<br>
				val_as("S4", -2147483648)
			</td>
			<td>
				129<br>
				0xfffe<br>
				0x80000000<br>
				0x00000080
			</td>
		</tr>
  </tbody>
</table>

[Table 1] `val_as()` 函数的支持格式

<table style="text-align:left">
	<thead>
		<tr>
			<th>字节序</th>
			<th>格式</th>
			<th>含义</th>
		</tr>
	</thead>
	<tbody>
		<tr><td rowspan="7">小<br>端</td>
		     <td>u1</td><td>无符号 1 字节</td></tr>
		<tr><td>u2</td><td>无符号 2 字节</td></tr>
		<tr><td>s1</td><td>有符号 1 字节</td></tr>
		<tr><td>s2</td><td>有符号 2 字节</td></tr>
		<tr><td>s4</td><td>有符号 4 字节</td></tr>
		<tr><td>f4</td><td>浮点数 4 字节</td></tr>
		<tr><td>f8</td><td>双精度浮点数 8 字节</td></tr>
		<tr><td rowspan="7">大<br>端</td>
		     <td>U1</td><td>无符号 1 字节</td></tr>
		<tr><td>U2</td><td>无符号 2 字节</td></tr>
		<tr><td>S1</td><td>有符号 1 字节</td></tr>
		<tr><td>S2</td><td>有符号 2 字节</td></tr>
		<tr><td>S4</td><td>有符号 4 字节</td></tr>
		<tr><td>F4</td><td>浮点数 4 字节</td></tr>
		<tr><td>F8</td><td>双精度浮点数 8 字节</td></tr>
	</tbody>
</table>