# 3.3.1 goto 문

### 설명

지정한 주소로 분기합니다.

### 문법

goto &lt;주소&gt;

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
      <td style="text-align:left">주소</td>
      <td style="text-align:left">
        <p>분기할 주소</p>
        <p>행 번호인 경우 산술식도
          가능</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
goto 99
goto addr
goto *err_hdl
```



