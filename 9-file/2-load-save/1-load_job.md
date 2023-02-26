# 9.2.1 load_job문

MAIN 모듈의 project/jobs/ 폴더의 변경사항을 새로 메모리로 읽어들이는 명령문입니다.

### 설명

MAIN 모듈의 project/jobs/ 폴더의 job들을 새로 메모리로 로드합니다.

FTP나 copyfile 명령으로 .job파일들을 jobs/ 폴더 내에 복사 혹은 overwrite한 경우, 이 명령문을 수행해주어야만 메모리로 반영되어 선택이나 call을 할 수 있습니다.

- 주의: jobs/ 폴더에 존재하지 않는 메모리 내의 job은 삭제됩니다.
- 수정된 시각이 달라진 파일이면 로드됩니다.
- 메모리에 존재하지 않는 파일이면 로드됩니다.

- 용량이 큰 .job들이 로드될 수 있기 때문에, 로드에 의한 택트 타임 손실이 없도록 백그라운드에서 비동기적으로 수행됩니다. 로드가 성공적으로 완료 되었는지는 결과변수의 값을 읽어 확인 할 수 있습니다.
- 로드가 끝나기 전에는 또 다른 로드를 요청할 수 없습니다.


### 문법

load_job &lt;결과변수&gt;,"*"

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
        <li>0: 로드 진행 중.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">job 파일명</td>
      <td style="text-align:left">
        모든 파일을 뜻하는 "*" 인수만을 사용할 수 있습니다.
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
     var res
     copyfile res,"project/vars","work/vars_1"
     wait res==1,8,*timeout
     copyfile res,"work/sub5.job","project/jobs/0005_sub.job"
     wait res==1,4,*timeout
     load_job res,"*"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "copyfile failed"
     end
```
