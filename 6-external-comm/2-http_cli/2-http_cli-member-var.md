# 6.2.2 멤버변수

<table>
  <thead>
    <tr>
      <th style="text-align:left">변수명</th>
      <th style="text-align:left">데이터형</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">body</td>
      <td style="text-align:left">모든 형 가능</td>
      <td style="text-align:left">
        <p>put과 post 요청에 실어보낼
          데이터를 미리 넣어두어야
          합니다.
        </p>
        <p>
          body에 object가 아닌 다른 형을 대입시에는 URL의 마지막 경로값을 Key로 처리하여 수행합니다.
        </p>
        <p>get과 post 요청의 응답이 보관됩니다.
          <br/>
        </p>
        <p>HRScript 에서는 직접적으로 body의 멤버변수에 접근을 할 수 없으므로, 해당 내용의 수정, 사용을 위해서는 다른 변수로 대입을 하여 사용 바랍니다.
          <br/>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">query</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">
        <p>
          query를 요구하는 get service에 사용됩니다.
          <br/>
          get 요청에 실어보낼 데이터를 미리 넣어 두어야합니다
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>
          http 통신 응답 코드와 에러 코드를 반환합니다. (6.2.4 HTTP 통신 코드)
          <br/>
        </p>
      </td>
    </tr>
  </tbody>
</table>

<br/>

body와 query는 object형이 사용됩니다.

object 형은 {key:value}의 형식으로 지원됩니다.

```python
cli.body = { name: "WORK #32", color: "green", state: "OK" }
cli.query = { axis: 3 }
```

