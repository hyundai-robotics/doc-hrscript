# 2.9.5 Other Functions

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
      <td style="text-align:left">cpo(crd, mode)</td>
      <td style="text-align:left">
        <p>Returns the current pose of the robot to the &#x201C;crd&#x201D; coordinate
          system</p>
        <p>For values that can be used as &#x201C;crd&#x201D; elements, see the table
          under &quot;<a href="../../moving-robot/pose.md">5.1 Pose</a>&quot;.</p>
        <p>If the mode is &#x201C;cmd,&#x201D; it is the command value, and if the
          mode is &#x201C;cur,&#x201D; it is the current value.</p>
        <p>The &#x201C;crd&#x201D; and &#x201C;mode&#x201D; parameters may be omitted,
          and their default values are &#x201C;base&#x201D; and &#x201C;cur,&#x201D;
          respectively.</p>
      </td>
      <td style="text-align:left">cpo(&quot;joint&quot;, &quot;cmd&quot;)</td>
      <td style="text-align:left">Pose* that stores the command value of the robot to the axis coordinate
        system</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)</p>
        <p>mkucs(n,po1,po2
          <br />,po3)</p>
      </td>
      <td style="text-align:left">
        <p>Creates and registers the nth user coordinate system object</p>
        <p>Refer to &quot;<a href="../../moving-robot/ucs.md">5.5 User Coordinate System (UCS)</a>&quot;.</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>0: OK</p>
        <p>&lt;0: Error code</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">For some procedures, it may be necessary to check the results. If the
        result() function is called right after the procedure is executed, the
        execution result can be returned.</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

\* Pose is a data type that represents the posture of the robot or the position of the tool tip. Details will be described later in "[5.1 Pose](../../5-moving-robot/1-pose.md)".

