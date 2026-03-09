# 5.22 scurve문

S-curve는 로봇 구동 시 발생하는 가속 및 감속 구간의 속도 변화를 곡선으로 처리하는 모션 궤적 계획 방식입니다.

- 기본 방식(Default): 가속 시작과 종료 시점에 속도가 급격하게 변하여 기계적 충격(Jerk)이 발생할 수 있습니다.
- S-curve 방식: 속도 변화를 부드럽게 만들어 장비의 진동을 최소화하고, 하드웨어 수명 연장 및 고속 구동 시 안정적인 경로 정확도를 확보합니다.

### 문법
```python
"scurve on, cnd=<조건번호>
"scurve off
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
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        S-curve 기능의 활성화 여부
      </td>
      <td style="text-align:left">on(켜기), off(끄기)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        cnd (조건 번호)
      </td>
      <td style="text-align:left">
        사용할 S-curve 조건의 번호 지정
      </td>
      <td style="text-align:left">1~16</td>
    </tr>
  </tbody>
</table>


### 사용 예
```python
     scurve on,cnd=1 # 1번 S-curve 조건 적용
S1   move P,tg=po1,spd=10%,accu=0,tool=0
     scurve off      # S-curve 적용 해제
S2   move P,tg=po1,spd=10%,accu=0,tool=0
     end
```

{% hint style="info" %}
자세한 내용은 ${cont_model} 제어기 조작설명서의 "[7.5.23 S-curve 조건](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/7-system/5-application-parameter/23-scurve-condition/README?cont_model=${cont_model})"를 참조하십시오.
{% endhint %}