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
        <p>返回机器人当前姿势到 "crd" 坐标系统</p>
        <p>有关可用作 "crd" 元素的值，请参见 "<a href="../../5-moving-robot/1-pose.md">5.1 姿势</a>" 下的表。</p>
        <p>如果模式为 "cmd"，则为命令值；如果模式为 "cur"，则为当前值。</p>
        <p>"crd" 和 "mode" 参数可以省略，默认值分别为 "base" 和 "cur"。</p>
      </td>
      <td style="text-align:left">cpo("joint", "cmd")</td>
      <td style="text-align:left">存储机器人到轴坐标系统的命令值的姿势*</td>
    </tr>
    <tr>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">通过执行 <a href="../../10-etc/1-proc/1-gather.md">gather</a> 语句返回当前数据收集状态</td>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">
        0 : 不在收集中。<br>
        1 : 在收集中。<br>
        2 : 正在将收集的结果保存为文件。
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)</p>
        <p>mkucs(n,po1,po2,po3)</p>
        <p>mkucs(n,"OXY",po1,po2,po3)</p>
      </td>
      <td style="text-align:left">
        <p>创建并注册第 n 个用户坐标系统对象</p>
        <p>请参阅 "<a href="../../5-moving-robot/5-mkucs.md">5.5 用户坐标系统 (UCS)</a>"。</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>0: 成功</p>
        <p>&lt;0: 错误代码</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">对于一些过程，检查结果可能是必要的。如果在执行过程后立刻调用 result() 函数，可以返回执行结果。</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
   <tr>
      <td style="text-align:left">mkshift(3,ref_po,mea_po,2.0) <br>
      mkshift(5,ref_po,mea_sft)
      </td>
      <td style="text-align:left">优化的移动值是根据多个参考姿势的测量姿势或移动数据计算并返回的。<br>
      如果第四个参数对应的容差被指定为大于 0，并且计算的移动值大于此值，则会停止并显示错误。<br>
      # 注意 <br>
      ref_po（参考姿势）和 mea_po（测量姿势）是姿势变量的数组类型，而 mea_sft（测量移动）是移动变量的数组类型。<br>
      如果没有对应于容差的第四个参数，则不会检测到错误。<br>
      我们目前支持最多 100 个位置。
      </td>
      <td style="text-align:left">sft1=mkshift(4,ref_po,mea_po,3.0)</td>
      <td style="text-align:left">移动</td>
    </tr> 
    <tr>
      <td style="text-align:left">calshift(po1,po2) <br>
      calshift(po1,po2,"TV")
      </td>
      <td style="text-align:left">返回两个姿势之间的差异作为移动值。<br>
      如果存在 "TV" 参数，则工具的垂直方向作为移动值返回。
      </td>
      <td style="text-align:left">sft1=calshift(po1,po2)</td>
      <td style="text-align:left">移动</td>
    </tr> 
    <tr>
      <td style="text-align:left">po.valid()
      </td>
      <td style="text-align:left">
        返回关于姿势对象的信息，以确定其是否在机器人的运动范围内。<br>
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
        返回关于姿势对象的信息，作为数组格式的字符串。<br>
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
        返回关于移动对象的信息，作为数组格式的字符串。<br>
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
        <p>执行 move ~ until 语句时，当满足 until 条件时，将返回当前姿势在 crd 坐标系统中的值。</p>
        <p>有关可用作 "crd" 元素的值，请参见 "<a href="../../5-moving-robot/1-pose.md">5.1 姿势</a>" 下的表。</p>
         <p>"crd" 参数可以省略，默认值为 "base"。</p>
      </td>
      <td style="text-align:left">upo(&quot;joint&quot;)
      </td>
      <td style="text-align:left">姿势*</td>
    </tr>

  </tbody>
</table>

\* 姿势是表示机器人姿态或工具尖端位置的数据类型。详细信息将在 "[5.1 姿势](../../5-moving-robot/1-pose.md)" 中描述。