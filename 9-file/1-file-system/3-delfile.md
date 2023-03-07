# 9.1.3 delfile문

delfile문은 디렉토리나 파일의 삭제를 요청하는 프로시져입니다.

### 설명

지정한 경로의 디렉토리, 혹은 파일을 삭제합니다.   

- 티치펜던트나 USB 메모리가 아닌 MAIN 모듈 내에서만 수행할 수 있습니다.
- 디렉토리의 서브 디렉토리들도 모두 삭제됩니다.
- 지정한 경로파일명이 존재하지 않으면, 성공으로 종료합니다.
- wildcard는 지원하지 않습니다.

- 용량이 큰 파일이나 디렉토리 전체가 삭제될 수도 있기 때문에, 삭제 중 대기에 의한 택트 타임 손실이 없도록 백그라운드에서 비동기적으로 수행됩니다. 삭제가 성공적으로 완료 되었는지는 결과변수의 값을 읽어 확인 할 수 있습니다.
- 하나의 복사나 삭제가 끝나기 전에는 다른 복사나 삭제를 요청할 수 없습니다.


### 문법

```python
delfile <결과변수>,<경로파일명>
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
      <td style="text-align:left">결과변수</td>
      <td style="text-align:left">
        백그라운드 수행 결과<br>
        <ul>
        <li>1: 성공적으로 완료됨.</li>
        <li>0: 삭제 진행 중.</li>
        <li>-1: 디렉토리 삭제 실패.</li>
        <li>-11: 파일 삭제 실패.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">경로파일명</td>
      <td style="text-align:left">
        삭제할 디렉토리 경로,<br>
        혹은 삭제할 파일의 경로파일명
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   var res
   delfile res,"work/vars_1"
   wait res==1,8,*timeout
   copyfile res,"project/jobs/0005_sub.job"
   wait res==1,4,*timeout
   end
   *timeout
   print "delfile failed"
   end
```
