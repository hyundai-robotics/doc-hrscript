# 5.6 contpath문

### 설명

CONTPATH(연속패스)의 모드를 선택합니다.

CONTPATH에 대한 설명은 아래 링크를 참조하십시오.  
[조작설명서: 8.15 R360 CONTPATH 수동 설정](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/8-r-code/15-r360)
<br><br>


### 문법

```python
contpath <모드 번호>
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
      <td style="text-align:left">모드 번호</td>
      <td style="text-align:left">
        0: 불연속<br>
        1: 연속모션. 입력신호는 불연속 (default)<br>
        2: 연속모션. 입력신호도 연속
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
contpath 0
```


{% hint style="info" %}

-	`contpath`문을 명시적으로 실행하지 않으면, 디폴트로 `contpath 1`이 적용됩니다. 명시적으로 지정한 경우에도 사이클 시작 시에는 `contpath 1` 로 초기화됩니다.

- 변경된 상태는 제목표시줄의 `CP0` / `CP1` / `CP2` 플래그로 확인할 수 있습니다.

{% endhint %}