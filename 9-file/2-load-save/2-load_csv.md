# 9.2.2 load_csv문

{% hint style="info" %}

MAIN 모듈의 project/vars/ 폴더의 .csv 파일(전역 최상위 배열)의 변경사항을 메모리로 읽어들이는 명령문입니다.

### 설명

HRScript의 전역 최상위(root) 배열은 vars/ 폴더에 CSV 표준형식의 파일로 저장됩니다. (최상위란 다른 배열이나 객체의 속성이 아닌 것을 의미합니다.)

변수 파일에 대한 관련 내용은 아래 조작설명서 링크를 참고하십시오.

[전역변수/변수 파일](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/6-monitoring/3-job/3-global-variable/3-var-files)

.csv 파일들은 PC에서 텍스트 편집기로 쉽게 편집할 수 있습니다.
편집된 파일을 vars/ 폴더로 복사하는 것 만으로는 즉각 메모리에 반영되지 않으며, 티치펜던트의 전역변수창에서 `[전부 불러오기]` 기능을 사용하거나, `load_csv` 명령을 실행해야만 반영됩니다.

- 용량이 큰 .csv들이 로드될 수 있기 때문에, 로드에 의한 택트 타임 손실이 없도록 백그라운드에서 비동기적으로 수행됩니다. 로드가 성공적으로 완료 되었는지는 결과변수의 값을 읽어 확인 할 수 있습니다.
- 로드가 끝나기 전에는 또 다른 로드를 요청할 수 없습니다.


### 문법

```python
load_csv <결과변수>,"*"
load_csv <결과변수>,"<변수명>"
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
        <li>1: 완료됨.</li>
        <li>0: 로드 진행 중.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">.csv 파일이름</td>
      <td style="text-align:left">
        <ul>
        <li>"*": 모든 파일 로드.</li>
        <li>"<변수명>": <변수명>.csv 파일을 로드.</li>
        </ul>
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
"*"을 지정하여 모든 .csv를 로드하면, vars/ 폴더에 .csv가 존재하지 않는 메모리 내의 최상위 배열들은 삭제됩니다.
{% endhint %}

### 사용 예

```python
     var res
     copyfile res,"work/arrs/locs1.csv","project/vars/locs.csv"
     wait res==1,4,*timeout
     load_csv res,"locs"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "failed to load new locations."
     end
```
