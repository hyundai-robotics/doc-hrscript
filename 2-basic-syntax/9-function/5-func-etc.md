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
        <p>Returns the current pose of the robot to the "crd" coordinate
          system</p>
        <p>For values that can be used as "crd" elements, see the table
          under "<a href="../../5-moving-robot/1-pose.md">5.1 Pose</a>".</p>
        <p>If the mode is "cmd," it is the command value, and if the mode is "cur," it is the current value.</p>
        <p>The "crd" and "mode" parameters may be omitted,
          and their default values are "base" and "cur,"
          respectively.</p>
      </td>
      <td style="text-align:left">cpo("joint", "cmd")</td>
      <td style="text-align:left">Pose* that stores the command value of the robot to the axis coordinate
        system</td>
    </tr>
    <tr>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">Returns the current state of data gathering by executing <a href="../../10-etc/1-proc/1-gather.md">gather</a> statement</td>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">
        0 : not in gathering.<br>
        1 : in gathering.<br>
        2 : saving the gathering result as a file.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)</p>
        <p>mkucs(n,po1,po2
          <br />,po3)</p>
      </td>
      <td style="text-align:left">
        <p>Creates and registers the nth user coordinate system object</p>
        <p>Refer to "<a href="../../5-moving-robot/5-ucs.md">5.5 User Coordinate System (UCS)</a>".</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>0: OK</p>
        <p>&lt;0: Error code</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">For some procedures, it may be necessary to check the results. If the result() function is called right after the procedure is executed, the execution result can be returned.</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

\* Pose is a data type that represents the posture of the robot or the position of the tool tip. Details will be described later in "[5.1 Pose](../../5-moving-robot/1-pose.md)".

