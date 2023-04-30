# 10.1.5 int_def문

int_def문은 인터럽트 조건과 감시 구간, 그리고 인터럽트 발생시 실행할 프로그램을 지정하는 프로시져입니다.

### 설명

인터럽트 기능이란 프로그램 호출의 한가지 종류입니다. 로봇이 인터럽트 감시 구간에서 작업할 경우, 기 정의된 인터럽트 조건을 만족하면 기 정의된 프로그램을 호출하여 실행합니다. 이 호출된 프로그램의 실행이 종료되면 다시 이전 실행하던 프로그램의 위치로 돌아와 계속 작업을 수행합니다.   

![](../../_assets/int_def_1.png)


### 기능 요약

- 인터럽트 감시 구간에서만 동작합니다.
- 인터럽트 조건식으로는 산술식을 모두 지원합니다.
- 인터럽트 프로그램 수행 중 또 다른 인터럽트 처리(다중 인터럽트)도 허용합니다.


### 인터럽트 삭제시점
하기의 조작이 발생되는 경우에는 모든 정의된 인터럽트가 자동으로 삭제됩니다.
- 'R0 : 태스크 리셋' 수행시
- 프로그램의 처음 실행시 
- 스텝이나 펑션 변경후 기동시


### 문법

```python
int_def <on/off>,no=<인터럽트 번호>,var=<인터럽트 조건>,val=<조건 일치값>,job=<호출 프로그램>,[once]
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
        인터럽트를 정의하거나 정의된 인터럽트를 삭제<br>
        <ul>
        <li>on: 새로운 인터럽트 정의.</li>
        <li>off: 정의된 인터럽트 삭제. (3번째 이후의 파라미터 무시됨)</li>
        </ul>
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
    <tr>
      <td style="text-align:left">인터럽트 번호</td>
      <td style="text-align:left">
        정의 또는 삭제할 인터럽트 번호를 지정<br>
      </td>
      <td style="text-align:left">산술식(1~8)</td>
    </tr>
    <tr>
      <td style="text-align:left">인터럽트 조건</td>
      <td style="text-align:left">
        인터럽트를 발생시킬 조건식을 정의<br>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">조건 일치값</td>
      <td style="text-align:left">
        인터럽트 발생을 위한 인터럽트의 조건식의 값<br>
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">호출 프로그램</td>
      <td style="text-align:left">
        인터럽트 발생시 호출할 프로그램 번호<br>
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">[once]</td>
      <td style="text-align:left">
        옵션 파라미터로 인터럽트 감시 구간내에서 인터럽트가 수회 발생하더라도 모두 처리하지 않고 처음 발생한 인터럽트 1회만 처리하고자 할때 사용<br>
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>


### 에러 가이드

- E1351 : 이미 정의된 인터럽트 번호에 대해서 삭제없이 재정의하는 경우에 발생합니다. 작성된 프로그램을 확인하십시오.


### 사용 예

```python
   int_def on,no=1,var=di5,val=1,job=24,once #인터럽트 정의
   move P,spd=30%,accu=3,tool=1
   move L,spd=30mm/s,accu=3,tool=1
   ...
   move L,spd=30mm/s,accu=3,tool=1
   move P,spd=30%,accu=3,tool=1
   int_def off,no=1 #인터럽트 삭제
   move P,spd=30%,accu=3,tool=1
   end
```


