# 4.2 Object

As previously seen, it was found that an array could store multiple element values and are accessed by index. 

Objects are like arrays in that they store multiple element values. The difference is that an object is accessed by a key, not with an index. Moreover, the key is a string, not a number. 

Objects are defined as var or global, like any other variables. The definition of an object and format of its access are as follows.

|  |  |
| :--- | :--- |
| Definition | var object name = { key : value, key : value, …} |
| Access | Object name key |



The following shows an example of defining and accessing an object.

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
        <p>var gap = { x:200, y:152.6 }</p>
        <p>gap.x = gap.x + 10</p>
        <p>print gap.x, gap.y</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">210 152.6</td>
    </tr>
  </tbody>
</table>



The object’s key must be in the format of an identifier, but the element’s value can be of any type and can also be of different types. 

An object can contain other objects or arrays as its elements. Likewise, an array can also contain other arrays or objects as its elements. In the following example, “work,” which is an object, contains “size,” which is an object, and “heights,” which is an array.

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
        <p>var work = { part_no:3, name: &quot;gear&quot;, tested : false</p>
        <p>, size : { x : 150, y : 80 }</p>
        <p>, heights : [ 72.89, 74.91, 81.03, 87.60, 87.11 ] }</p>
        <p>print work.tested, work.size.y, work.heights[3]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Result</td>
      <td style="text-align:left">false, 80, 87.600000</td>
    </tr>
  </tbody>
</table>



