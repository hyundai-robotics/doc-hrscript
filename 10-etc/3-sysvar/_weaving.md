# _weaving 문

### 설명

_weaving문은 현재 선택된 위빙 조건을 변경하기 위해서 사용합니다.

### 문법

```python
_weaving.frequency=2
_weaving.angle=5
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">weave</td>
      <td style="text-align:left">
         위빙 형태 (0=단진동, 1=삼각, 2=L형, 3=원형)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">frequency</td>
      <td style="text-align:left">
        주파수[Hz]
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">left_distance</td>
      <td style="text-align:left">
        벽방향 거리[mm]
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">right_distance</td>
      <td style="text-align:left">
        타방향 거리[mm]
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">angle</td>
      <td style="text-align:left">
        각도[deg]
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">offset_angle</td>
      <td style="text-align:left">
        옵셋 각도[deg]
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">wall_direction</td>
      <td style="text-align:left">
        벽방향 (0=수직, 1=수평, 2=토치 자세기준)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">forward_angle</td>
      <td style="text-align:left">
        진행각도[deg]
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">boundary_limit</td>
      <td style="text-align:left">
        경계제한 (0=유효, 1=무효)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_time_1</td>
      <td style="text-align:left">
        구간 (1~4) 이동시간[s]
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">segment_delay_1</td>
      <td style="text-align:left">
        구간 (1~4) 타이머(위빙정지)[s]
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_mode</td>
      <td style="text-align:left">
        높이센싱 모드 (0=전류변화, 1=좌측 고정, 2=우측 고정)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_mode</td>
      <td style="text-align:left">
        좌우센싱 모드 (0=중심선, 1=왼쪽, 2=오른쪽)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">asymetric_sensing_ratio</td>
      <td style="text-align:left">
        비대칭 센싱 비율 (-50~50) [%]
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">side_sensing_sensitivity</td>
      <td style="text-align:left">
        좌우센싱 민감도 (0~10)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">height_sensing_sensitivity</td>
      <td style="text-align:left">
        높이센싱 민감도 (0~10)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>




### 사용 예

```python
   weaving on,cnd=1
   move P,spd=50%,accu=3,tool=1
   _weaving.frequency=5    # 위빙주파수를 5Hz로 변경
   move P,spd=50%,accu=3,tool=1
   weaving off
   end
```

