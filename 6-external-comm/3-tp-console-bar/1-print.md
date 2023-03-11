# 6.3.1 print문

### 설명

print문을 통해 티치펜던트의 안내표시줄에 문자열을 출력합니다. 문자열 상수 뿐만 아니라, 어떤 타입의 표현식(상수, 변수 포함)을 지정해도 그 결과를 문자열로 변환하여 출력합니다. 표현식을 여러 개 지정하면 각 표현식들을 공백 1글자로 구분하여 출력합니다.

### 문법

```python
print <표현식>[,<표현식>,<표현식>...]
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
      <td style="text-align:left">표현식 (expression)</td>
      <td style="text-align:left">
        <p>출력할 표현식. 논리, 숫자, 문자열, 배열, 객체의 모든 타입을 지원합니다.
          <br
          />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
print "hello, world"
print arr[0],arr[1],arr[2]
print "x-center: "+(width/2), "y-center: "+(height/2)
print po10+sft21
```
