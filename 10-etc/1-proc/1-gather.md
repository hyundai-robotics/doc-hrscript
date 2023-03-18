# 10.1.1 gather문

gather문은 데이터 수집 기능을 사용할 때 데이터 수집 시작과 종료 위치를 지정하는 프로시져입니다.

### 설명

gather를 통해 데이터를 수집 시작과 종료를 지정합니다. 수집 결과 파일은 아래와 같이 저장됩니다.
- 저장 경로: MAIN/project
- 파일명: 0001.GDT ~ 0030.GDT

수집 결과 파일은  최대 30개까지 저장되며, 개수 초과 시 이전 수집 결과 파일을 덮어써서 저장됩니다.


### 문법

```python
gather <시작/종료>
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
      <td style="text-align:left">시작/종료</td>
      <td style="text-align:left">
        선택할 사용자 좌표계 번호<br>
        <ul>
        <li>1: 데이터 수집 시작</li>
        <li>0: 데이터 수집 종료</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
S1   move L,spd=100%,accu=0,tool=0
     gather 1
S2   move L,spd=100%,accu=0,tool=0
     delay 1.5
S3   move L,spd=100%,accu=0,tool=0
     gather 0
     end
```