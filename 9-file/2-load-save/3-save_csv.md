# 9.2.3 save_csv문

{% hint style="info" %}

* V60.28-00부터 지원됩니다.

{% endhint %}

전역 최상위 배열 변수를 메모리에서 MAIN 모듈의 project/vars/ 폴더의 .csv 파일로 저장하는 명령문입니다.

### 설명

HRScript의 전역 최상위(root) 배열은 vars/ 폴더에 CSV 표준형식의 파일로 저장됩니다. (최상위란 다른 배열이나 객체의 속성이 아닌 것을 의미합니다.)

변수 파일에 대한 관련 내용은 아래 조작설명서 링크를 참고하십시오.

[전역변수/변수 파일](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-${cont_model}-tp630/6-monitoring/3-job/3-global-variable/3-var-files)

전역 최상위(root) 배열은 값이 바뀔 때마다 즉각적으로 .csv 파일에 저장되지는 않습니다.
`Ctrl+[F7: save]`를 누르거나 전원을 끌 때에 파일로 저장되는데, `save_csv` 명령문을 수행하면 즉각 파일로 저장할 수 있습니다.

- 용량이 큰 .csv들이 저장될 수 있기 때문에, 저장에 의한 택트 타임 손실이 없도록 백그라운드에서 비동기적으로 수행됩니다. 저장이 성공적으로 완료 되었는지는 결과변수의 값을 읽어 확인 할 수 있습니다.
- 저장이 끝나기 전에는 또 다른 저장을 요청할 수 없습니다.


### 문법

```python
save_csv <결과변수>,"*"
save_csv <결과변수>,"<변수명>"
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
        <li>0: 저장 진행 중.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">.csv 파일이름</td>
      <td style="text-align:left">
        <ul>
        <li>"*": 모든 최상위 배열 변수 저장.</li>
        <li>"<변수명>": 지정한 변수를 .csv 파일로 저장.</li>
        </ul>
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
"*"을 지정하여 모든 .csv를 저장하는 경우, 대응하는 이름의 최상위 변수가 존재하지 않는다고 해서, vars/ 폴더에 있던 .csv 파일을 삭제하지는 않습니다.
{% endhint %}

### 사용 예

```python
     var res
     save_csv res,"locs"
     wait res==1,4,*timeout
     copyfile res,"project/vars/locs.csv","work/arrs/locs2.csv"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "failed to save new locations."
     end
```
