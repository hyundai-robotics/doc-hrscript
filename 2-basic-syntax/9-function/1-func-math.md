# 2.9.1 Math Functions

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Example of usage</th>
      <th style="text-align:left">Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">abs(<b>a</b>)</td>
      <td style="text-align:left">Returns the absolute value of <b>a</b>
      </td>
      <td style="text-align:left">abs(-300)</td>
      <td style="text-align:left">300</td>
    </tr>
    <tr>
      <td style="text-align:left">acos(<b>a</b>)</td>
      <td style="text-align:left">Returns the arc cosine value of <b>a</b> in radian format</td>
      <td style="text-align:left">acos(0.5)</td>
      <td style="text-align:left">1.0472</td>
    </tr>
    <tr>
      <td style="text-align:left">asin(<b>a</b>)</td>
      <td style="text-align:left">Returns the arc sine value of <b>a</b> in radian format</td>
      <td style="text-align:left">asin(0.5)</td>
      <td style="text-align:left">0.5236</td>
    </tr>
    <tr>
      <td style="text-align:left">atan(<b>a</b>)</td>
      <td style="text-align:left">Returns the arctangent value of <b>a</b> in radian format</td>
      <td style="text-align:left">atan(0.5)</td>
      <td style="text-align:left">0.4636</td>
    </tr>
    <tr>
      <td style="text-align:left">atan2(<b>a</b>, <b>b</b>)</td>
      <td style="text-align:left">Returns the arctangent value of a triangle with <b>a</b> for the y length
        and <b>b</b> for the x length in radian format</td>
      <td style="text-align:left">atan2(2,1)</td>
      <td style="text-align:left">1.1071</td>
    </tr>
    <tr>
      <td style="text-align:left">cos(<b>r</b>)</td>
      <td style="text-align:left">Returns the cosine value of <b>r</b> in radian format</td>
      <td style="text-align:left">cos(3.1415)</td>
      <td style="text-align:left">-1</td>
    </tr>
    <tr>
      <td style="text-align:left">deg2rad(<b>d</b>)</td>
      <td style="text-align:left">Returns the radian value of <b>d</b> in degree format</td>
      <td style="text-align:left">deg2rad(-90)</td>
      <td style="text-align:left">-1.570796</td>
    </tr>
    <tr>
      <td style="text-align:left">dist(<b>x</b>, <b>y</b>)</td>
      <td style="text-align:left">Returns the Euclidean distance from the origin to the (<b>x</b>, <b>y</b>)
        coordinate</td>
      <td style="text-align:left">dist(3.5,10)</td>
      <td style="text-align:left">10.59481</td>
    </tr>
    <tr>
      <td style="text-align:left">max(<b>a</b>, <b>b</b>)</td>
      <td style="text-align:left">Returns the greater value between <b>a</b> and <b>b</b>
      </td>
      <td style="text-align:left">max(-1.23, -3)</td>
      <td style="text-align:left">-1.23</td>
    </tr>
    <tr>
      <td style="text-align:left">min(<b>a</b>, <b>b</b>)</td>
      <td style="text-align:left">Returns the lesser value between <b>a</b> and <b>b</b>
      </td>
      <td style="text-align:left">max(-1.23, -3)</td>
      <td style="text-align:left">-3</td>
    </tr>
    <tr>
      <td style="text-align:left">near(<b>a</b>, <b>b</b> [,<b>e</b>])</td>
      <td style="text-align:left">Returns 1 if the difference between the real number values &#x200B;&#x200B;<b> a</b> and <b>b</b> is
        less than or equal to <b>e</b> and returns 0 if the difference is larger
        than <b>e</b>
      </td>
      <td style="text-align:left">
        <p>near(0.005, 0.0058)</p>
        <p>near(0.005, 0.006)</p>
        <p>near(0.005, 0.006, 0.1)</p>
      </td>
      <td style="text-align:left">
        <p>1</p>
        <p>0</p>
        <p>1</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rad2deg(<b>r</b>)</td>
      <td style="text-align:left">Returns the degree value of <b>r</b> in radian format</td>
      <td style="text-align:left">rad2deg(1.570796)</td>
      <td style="text-align:left">90</td>
    </tr>
    <tr>
      <td style="text-align:left">sin(<b>r</b>)</td>
      <td style="text-align:left">Returns the sine value of <b>r</b> in radian format</td>
      <td style="text-align:left">sin(1.5*3.1415)</td>
      <td style="text-align:left">-1</td>
    </tr>
    <tr>
      <td style="text-align:left">sqr(<b>a</b>)</td>
      <td style="text-align:left">Returns the square root of <b>a</b>
      </td>
      <td style="text-align:left">
        <p>sqr(16)</p>
        <p>sqr(0)</p>
      </td>
      <td style="text-align:left">
        <p>4</p>
        <p>0</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">tan(<b>r</b>)</td>
      <td style="text-align:left">Returns the tangent value of <b>r</b> in radian format</td>
      <td style="text-align:left">tan(3.141592/4)</td>
      <td style="text-align:left">0.9999</td>
    </tr>
  </tbody>
</table>





