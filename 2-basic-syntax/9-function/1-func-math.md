# 2.9.1 Math Functions

<table style="text-align:left">
  <thead>
    <tr>
      <th>Function</th>
      <th>Description</th>
      <th>Example of usage</th>
      <th>Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>abs(<b>a</b>)</td>
      <td>Returns the absolute value of <b>a</b>
      </td>
      <td>abs(-300)</td>
      <td>300</td>
    </tr>
    <tr>
      <td>acos(<b>a</b>)</td>
      <td>Returns the arc cosine value of <b>a</b> in radian format</td>
      <td>acos(0.5)</td>
      <td>1.0472</td>
    </tr>
    <tr>
      <td>asin(<b>a</b>)</td>
      <td>Returns the arc sine value of <b>a</b> in radian format</td>
      <td>asin(0.5)</td>
      <td>0.5236</td>
    </tr>
    <tr>
      <td>atan(<b>a</b>)</td>
      <td>Returns the arctangent value of <b>a</b> in radian format</td>
      <td>atan(0.5)</td>
      <td>0.4636</td>
    </tr>
    <tr>
      <td>atan2(<b>a</b>, <b>b</b>)</td>
      <td>Returns the arctangent value of a triangle with <b>a</b> for the y length
        and <b>b</b> for the x length in radian format</td>
      <td>atan2(2,1)</td>
      <td>1.1071</td>
    </tr>
		<tr>
			<td>ceil(x)</td>
			<td>Returns the rounded up value of <b>x</b>.</td>
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
      <td>Returns the cosine value of <b>r</b> in radian format</td>
      <td>cos(3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>deg2rad(<b>d</b>)</td>
      <td>Returns the radian value of <b>d</b> in degree format</td>
      <td>deg2rad(-90)</td>
      <td>-1.570796</td>
    </tr>
    <tr>
      <td>dist(<b>x</b>, <b>y</b>)</td>
      <td>Returns the Euclidean distance from the origin to the (<b>x</b>, <b>y</b>)
        coordinate</td>
      <td>dist(3.5,10)</td>
      <td>10.59481</td>
    </tr>
		<tr>
			<td>floor(x)</td>
			<td>Returns the rounded down value of <b>x</b>.</td>
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
      <td>Returns the greater value between <b>a</b> and <b>b</b>
      </td>
      <td>max(-1.23, -3)</td>
      <td>-1.23</td>
    </tr>
    <tr>
      <td>min(<b>a</b>, <b>b</b>)</td>
      <td>Returns the lesser value between <b>a</b> and <b>b</b>
      </td>
      <td>max(-1.23, -3)</td>
      <td>-3</td>
    </tr>
    <tr>
      <td>near(<b>a</b>, <b>b</b> [,<b>e</b>])</td>
      <td>Returns 1 if the difference between the real number values &#x200B;&#x200B;<b> a</b> and <b>b</b> is
        less than or equal to <b>e</b> and returns 0 if the difference is larger
        than <b>e</b>
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
      <td>Returns the degree value of <b>r</b> in radian format</td>
      <td>rad2deg(1.570796)</td>
      <td>90</td>
    </tr>
		<tr>
			<td>round(x)</td>
			<td>Returns the rounded off value of <b>x</b>.</td>
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
      <td>Returns the sine value of <b>r</b> in radian format</td>
      <td>sin(1.5*3.1415)</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>sqr(<b>a</b>)</td>
      <td>Returns the square root of <b>a</b>
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
      <td>Returns the tangent value of <b>r</b> in radian format</td>
      <td>tan(3.141592/4)</td>
      <td>0.9999</td>
    </tr>
		<tr>
			<td>trunc(x)</td>
			<td>Returns the the truncated integer part of <b>x</b>.</td>
			<td>
				trunc(3.1415)<br>
				trunc(-3.1415)
			</td>
			<td>
				3<br>
				-3
			</td>
		</tr>
  </tbody>
</table>





