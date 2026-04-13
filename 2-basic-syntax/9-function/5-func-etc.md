# 2.9.5 其他功能

<table>
  <thead>
    <tr>
      <th style="text-align:left">功能</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">使用示例</th>
      <th style="text-align:left">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">cpo(crd, mode)</td>
      <td style="text-align:left">
        <p>返回机器人的当前姿态到"crd"坐标系</p>
        <p>有关可以作为"crd"元素使用的值，请参见 "<a href="../../5-moving-robot/1-pose.md">5.1 姿态</a>" 下的表格。</p>
        <p>如果模式为"cmd"，则为命令值；如果模式为"cur"，则为当前值。</p>
        <p>"crd"和"mode"参数可以省略，它们的默认值分别为"base"和"cur"。</p>
      </td>
      <td style="text-align:left">cpo("joint", "cmd")</td>
      <td style="text-align:left">姿态*，保存机器人的命令值到轴坐标系</td>
    </tr>
    <tr>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">通过执行 <a href="../../10-etc/1-proc/1-gather.md">gather</a> 语句返回当前的数据收集状态</td>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">
        0 : 不在收集状态。<br>
        1 : 在收集状态。<br>
        2 : 将收集结果保存为文件。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)</p>
        <p>mkucs(n,po1,po2,po3)</p>
        <p>mkucs(n,"OXY",po1,po2,po3)</p>
      </td>
      <td style="text-align:left">
        <p>创建并注册第 n 个用户坐标系对象</p>
        <p>请参考 "<a href="../../5-moving-robot/5-mkucs.md">5.5 用户坐标系统 (UCS)</a>"。</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
<p>0: 好</p>
        <p>&lt;0: 错误代码</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">对于某些程序，可能需要检查结果。如果在执行程序之后立即调用result()函数，则可以返回执行结果。</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
   <tr>
      <td style="text-align:left">mkshift(3,ref_po,mea_po,2.0) <br>
      mkshift(5,ref_po,mea_sft)
      </td>
      <td style="text-align:left">优化的偏移值是根据多个参考姿势的测量姿势或偏移数据计算并返回的。 <br>
      如果指定的与公差相关的第4个参数大于0，并且计算的偏移值大于该值，则会停止并报告错误。 <br>
      # 注 <br>
      ref_po（参考姿势）和 mea_po（测量姿势）是姿势变量的数组类型，mea_sft（测量偏移）是偏移变量的数组类型。 <br>
      如果没有与公差相关的第4个参数，则不会检测到错误。 <br>
      我们目前支持最多100个位置。
      </td>
      <td style="text-align:left">sft1=mkshift(4,ref_po,mea_po,3.0)</td>
      <td style="text-align:left">偏移</td>
    </tr> 
    <tr>
      <td style="text-align:left">calshift(po1,po2) <br>
      calshift(po1,po2,"TV")
      </td>
      <td style="text-align:left">返回两个姿势之间的差异作为偏移值。 <br>
      如果存在“TV”参数，则返回工具的垂直方向作为偏移值。
      </td>
      <td style="text-align:left">sft1=calshift(po1,po2)</td>
      <td style="text-align:left">偏移</td>
    </tr> 
    <tr>
      <td style="text-align:left">po.valid()
      </td>
      <td style="text-align:left">
        返回与机器人的运动范围内姿势对象有关的信息。 <br>
        # 示例 <br>
        if po1.valid()==0 <br>
            stop # 机器人停止<br>
        endif <br>        
      </td>
      <td style="text-align:left">var ret=po1.valid()
      </td>
      <td style="text-align:left">0: 超出操作范围 <br>
      1: 在操作范围内
      </td>
    </tr>
<tr>
      <td style="text-align:left">po.str_array()
      </td>
      <td style="text-align:left">
        返回关于姿态对象的信息，以数组格式的字符串形式表示。 <br>
        # 示例 <br>
        var msg=cpo().str_array() <br>
        print msg # [1850.000,2010.500,0.000,0.000,-90.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=po1.str_array()
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
    <tr>
      <td style="text-align:left">sft.str_array()
      </td>
      <td style="text-align:left">
        返回关于位移对象的信息，以数组格式的字符串形式表示。 <br>
        # 示例 <br>
        var sft1=Shift(0.000,0.000,30.000,0.000,0.000,0.000,"base") <br>
        var msg=sft1.str_array() <br>
        print msg # [0.000,0.000,30.000,0.000,0.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=sft1.str_array()
      </td>
      <td style="text-align:left">字符串</td>
    </tr>
    <tr>
      <td style="text-align:left">upo(crd)
      </td>
      <td style="text-align:left">
        <p>在执行移动 ~ 直到语句时，当直到条件满足时返回当前姿态，返回值为crd坐标系。</p>
        <p>有关可以用作“crd”元素的值，请参见
          "<a href="../../5-moving-robot/1-pose.md">5.1 姿态</a>" 下的表格。</p>
         <p>“crd”参数可以省略，默认值为“base”。</p>
      </td>
      <td style="text-align:left">upo(&quot;joint&quot;)
      </td>
      <td style="text-align:left">姿态*</td>
    </tr>

  </tbody>
</table>

\* 姿态是一种数据类型，表示机器人姿态或工具尖端的位置。详细信息将在"[5.1 姿态](../../5-moving-robot/1-pose.md)"中描述。