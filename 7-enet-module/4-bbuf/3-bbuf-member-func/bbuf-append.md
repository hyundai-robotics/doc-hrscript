# append

### 설명

바이너리 버퍼에 지정된 형식(format)으로 데이터를 추가합니다.


### 문법

{BBuf객체}.append {format}, {data}


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
      <td style="text-align:left">format</td>
      <td style="text-align:left">
			바이너리 데이터 형식(format)*<br>
      e.g. "U4", "s2"
      </td>
      <td style="text-align:left">문자열형</td>
    </tr>
	 <tr>
      <td style="text-align:left">data</td>
      <td style="text-align:left">
        바이너리 버퍼에 추가할 데이터
      </td>
      <td style="text-align:left">기본형(primitive) 데이터,<br>혹은 기본형 데이터의 1차원 배열</td>
    </tr>
  </tbody>
</table>

<br>


\* [7.4.2 지원 형식 (format)](../2-format.md)을 참조하십시오.
<br>
<br>


### 리턴값

추가된 데이터의 개수


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
```
