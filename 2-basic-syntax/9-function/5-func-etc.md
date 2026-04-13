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
        <p>mkucs(n,po1,po2,po3)</p>
        <p>mkucs(n,"OXY",po1,po2,po3)</p>
      </td>
      <td style="text-align:left">
        <p>Creates and registers the nth user coordinate system object</p>
        <p>Refer to "<a href="../../5-moving-robot/5-mkucs.md">5.5 User Coordinate System (UCS)</a>".</p>
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
   <tr>
      <td style="text-align:left">mkshift(3,ref_po,mea_po,2.0) <br>
      mkshift(5,ref_po,mea_sft)
      </td>
      <td style="text-align:left">The optimized shift value is calculated and returned from the measured pose or shift data corresponding to multiple reference poses. <br>
      If the 4th parameter corresponding to tolerance is specified to be greater than 0 and the calculated shift value is greater than this value, it stops with an error. <br>
      # Note <br>
      ref_po (reference pose) and mea_po (measured pose) are the array types of pose variables, and mea_sft (measured shift) is the type of array of shift variables. <br>
      If there is no 4th parameter corresponding to tolerance, no error is detected. <br>
      We currently support up to 100 positions.
      </td>
      <td style="text-align:left">sft1=mkshift(4,ref_po,mea_po,3.0)</td>
      <td style="text-align:left">Shift</td>
    </tr> 
    <tr>
      <td style="text-align:left">calshift(po1,po2) <br>
      calshift(po1,po2,"TV")
      </td>
      <td style="text-align:left">Returns the difference between two poses as a shift value. <br>
      If the "TV" parameter is present, the vertical orientation of the tool is returned as a shift value.
      </td>
      <td style="text-align:left">sft1=calshift(po1,po2)</td>
      <td style="text-align:left">Shift</td>
    </tr> 
    <tr>
      <td style="text-align:left">po.valid()
      </td>
      <td style="text-align:left">
        Returns information about the pose object whether it is within the robot's motion range. <br>
        # Example <br>
        if po1.valid()==0 <br>
            stop # Robot stop<br>
        endif <br>        
      </td>
      <td style="text-align:left">var ret=po1.valid()
      </td>
      <td style="text-align:left">0:Outside the operating range <br>
      1:Within operating range
      </td>
    </tr>
    <tr>
      <td style="text-align:left">po.str_array()
      </td>
      <td style="text-align:left">
        Returns information about the pose object as a string in array format. <br>
        # Example <br>
        var msg=cpo().str_array() <br>
        print msg # [1850.000,2010.500,0.000,0.000,-90.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=po1.str_array()
      </td>
      <td style="text-align:left">String</td>
    </tr>
    <tr>
      <td style="text-align:left">sft.str_array()
      </td>
      <td style="text-align:left">
        Returns information about the shift object as a string in array format. <br>
        # Example <br>
        var sft1=Shift(0.000,0.000,30.000,0.000,0.000,0.000,"base") <br>
        var msg=sft1.str_array() <br>
        print msg # [0.000,0.000,30.000,0.000,0.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=sft1.str_array()
      </td>
      <td style="text-align:left">String</td>
    </tr>
    <tr>
      <td style="text-align:left">upo(crd)
      </td>
      <td style="text-align:left">
        <p>When executing the move ~ until statement, the current pose when the until condition is satisfied is returned in the crd coordinate system.</p>
        <p>For values that can be used as "crd" elements, see the table
          under "<a href="../../5-moving-robot/1-pose.md">5.1 Pose</a>".</p>
         <p>The "crd" parameter may be omitted,
          and the default value is "base" respectively.</p>
      </td>
      <td style="text-align:left">upo(&quot;joint&quot;)
      </td>
      <td style="text-align:left">Pose*</td>
    </tr>

  </tbody>
</table>

\* Pose is a data type that represents the posture of the robot or the position of the tool tip. Details will be described later in "[5.1 Pose](../../5-moving-robot/1-pose.md)".

