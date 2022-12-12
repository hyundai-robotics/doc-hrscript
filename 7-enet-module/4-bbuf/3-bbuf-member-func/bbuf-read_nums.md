# read_nums

### 설명

바이너리 버퍼의 지정 위치로부터 지정한 개수의 숫자형 값을 읽어 배열 형식으로 리턴합니다.


### 문법

`{BBuf객체}.read_num  {format},{offset},{n.item}`


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
			바이너리 데이터 형식(format)<sup>*</sup><br>
      e.g. "U4", "s2"
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
    <tr>
      <td style="text-align:left">n.item</td>
      <td style="text-align:left">
        읽을 데이터 개수
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

* 읽은 숫자형 값들의 배열.  
* 만일 버퍼에 있는 데이터의 개수가 지정한 개수보다 적으면, 있는 만큼만 읽습니다.
* 만일 데이터 형식을 읽을 때 오류가 발생하면 빈 배열을 리턴합니다.


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_nums("U4", 12, 3) # "[3, 5, 7]"
print bbuf.read_num("U4", 12, 6) # "[3, 5, 7, 11, 13]"
```
