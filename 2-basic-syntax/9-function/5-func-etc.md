# 2.9.5 기타 함수



<table>
  <thead>
    <tr>
      <th style="text-align:left">함수</th>
      <th style="text-align:left">설명</th>
      <th style="text-align:left">사용 예</th>
      <th style="text-align:left">결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">cpo(crd, mode)
      </td>
      <td style="text-align:left">
        로봇이 취하고 있는 현재 자세(current pose)를 crd좌표계로 리턴합니다.
        crd 인수로 사용할 수 있는 값은 &quot;<a href="../../5-moving-robot/1-pose.md">5.1 포즈 (pose)</a>&quot;의 표를 참조하십시오.
        mode가 "cmd"이면 지령값, "cur"이면 현재값입니다.
        crd, mode 파라미터를 생략 가능하며 디폴트값은 각각 "base", "cur" 입니다.
      </td>
      <td style="text-align:left">cpo(&quot;joint&quot;, &quot;cmd&quot;)
      </td>
      <td style="text-align:left">로봇의 지령값을 축좌표계로 보관하는 포즈*</td>
    </tr>
    <tr>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left"><a href="../../10-etc/1-proc/1-gather.md">gather문</a> 수행에 의한 데이터 수집 동작의 현재 상태를 리턴 받을 수 있습니다.</td>
      <td style="text-align:left">gather_state()</td>
      <td style="text-align:left">
        0 : 미수행 중.<br>
        1 : 수행 중.<br>
        2 : 결과를 file로 저장 중.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        mkucs(n,po)<br>
        mkucs(n,po1,po2,po3)
      </td>
      <td style="text-align:left">
        n번 사용자좌표계 객체를 생성하여 등록합니다.<br>
        &quot;<a href="../../5-moving-robot/5-mkucs.md">5.5 사용자좌표계 (UCS ; User Coordinate System)</a>&quot;를 참조하십시오.
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        0 : OK<br>
        &lt;0 : 에러코드
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">일부 프로시져는 수행
        결과를 확인해야 할 경우가 있습니다. 프로시져 수행 직후 result( ) 함수를 호출하면, 수행 결과를 리턴 받을 수 있습니다.</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">mkshift(3,ref_po,mea_po,2.0) <br>
      mkshift(5,ref_po,mea_sft)
      </td>
      <td style="text-align:left">다수의 기준이 되는 포즈에 해당하는 측정된 포즈나 쉬프트 데이터들로 부터 최적화된 쉬프트 값을 계산하여 리턴합니다. <br>
      tolerance에 해당하는 4번째 파라미터가 0보다 크게 지정된 경우에 계산된 쉬프트 값이 이 값보다 크면 에러로 정지합니다. <br>
      # 참고 사항 <br>
      ref_po(기준이 되는 포즈), mea_po(측정된 포즈)는 포즈 변수의 배열, mea_sft(측정된 쉬프트)는 쉬프트 변수의 배열의 타입입니다. <br>
      tolerance에 해당하는 4번째 파라미터가 없으면 에러를 검지하지 않습니다. <br>
      현재 지원하는 위치는 최대 100개입니다.
      </td>
      <td style="text-align:left">sft1=mkshift(4,ref_po,mea_po,3.0)</td>
      <td style="text-align:left">쉬프트</td>
    </tr> 
    <tr>
      <td style="text-align:left">calshift(po1,po2) <br>
      calshift(po1,po2,"TV")
      </td>
      <td style="text-align:left">2개의 포즈간의 차이를 쉬프트 값으로 리턴합니다. <br>
      "TV" 파라미터가 있으면 툴의 수직 방향의 자세를 쉬프트 값으로 리턴합니다.
      </td>
      <td style="text-align:left">sft1=calshift(po1,po2)</td>
      <td style="text-align:left">쉬프트</td>
    </tr> 
    <tr>
      <td style="text-align:left">po.valid()
      </td>
      <td style="text-align:left">
        포즈 객체에 대한 정보가 로봇의 동작범위 내에 있는지 리턴합니다. <br>
        # 사용 예 <br>
        if po1.valid()==0 <br>
            stop # 로봇 정지<br>
        endif <br>        
      </td>
      <td style="text-align:left">var ret=po1.valid()
      </td>
      <td style="text-align:left">0:동작범위 밖 <br>
      1:동작범위 내
      </td>
    </tr>
    <tr>
      <td style="text-align:left">po.str_array()
      </td>
      <td style="text-align:left">
        포즈 객체에 대한 정보를 배열 형식의 문자열로 리턴합니다. <br>
        # 사용 예 <br>
        var msg=cpo().str_array() <br>
        print msg # [1850.000,2010.500,0.000,0.000,-90.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=po1.str_array()
      </td>
      <td style="text-align:left">문자열</td>
    </tr>
    <tr>
      <td style="text-align:left">sft.str_array()
      </td>
      <td style="text-align:left">
        쉬프트 객체에 대한 정보를 배열 형식의 문자열로 리턴합니다. <br>
        # 사용 예 <br>
        var sft1=Shift(0.000,0.000,30.000,0.000,0.000,0.000,"base") <br>
        var msg=sft1.str_array() <br>
        print msg # [0.000,0.000,30.000,0.000,0.000,0.000,"base"]
      </td>
      <td style="text-align:left">msg=sft1.str_array()
      </td>
      <td style="text-align:left">문자열</td>
    </tr>
    <tr>
      <td style="text-align:left">upo(crd)
      </td>
      <td style="text-align:left">
        move ~ until문 수행시 until 조건이 만족했을 때의 현재 자세(current pose)를 crd좌표계로 리턴합니다.
        crd 인수로 사용할 수 있는 값은 &quot;<a href="../../5-moving-robot/1-pose.md">5.1 포즈 (pose)</a>&quot;의 표를 참조하십시오.
        crd 파라미터를 생략 가능하며 디폴트값은 각각 "base" 입니다.
      </td>
      <td style="text-align:left">upo(&quot;joint&quot;)
      </td>
      <td style="text-align:left">로봇의 포즈*</td>
    </tr>

  </tbody>
</table>

\* 포즈\(pose\)는 로봇의 자세 혹은 툴 끝의 위치를 나타내는 데이터형입니다. 이후의 "[5.1 포즈 \(pose\)](../../5-moving-robot/1-pose.md)"에서 자세히 설명합니다.

