# read_num

### 설명

바이너리 버퍼의 지정 위치로부터 숫자형 값을 읽어 리턴합니다.


### 문법

{BBuf객체}.read_num {format}, {offset}


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
      e.g. "U4", "s2"<br>
      </td>
      <td style="text-align:left">문자열형</td>
    </tr>
	 <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        데이터를 읽을 위치 (0-based byte offset)
      </td>
      <td style="text-align:left">정수형</td>
    </tr>
  </tbody>
</table>

<br>

\* [7.4.2 지원 형식 (format)](../2-format.md)을 참조하십시오.
<br>
<br>

### 리턴값

* 읽은 숫자형 값
* 만일 데이터 형식을 읽을 때 오류가 발생하면 0을 리턴합니다.


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_num("F8", 0) # "9.80665"
print bbuf.read_num("U4", 12) # "3"
print bbuf.read_num("U4", 16) # "5"
```
