# 3.7.3 jump문

### 설명

jump 문의 형식은 아래와 같습니다. 

### 문법

```python
jump <JOB번호 혹은 파일이름> [,매개변수1,매개변수2,…]
```

형식이 call문과 완전히 동일하며 동작도 유사합니다.

유일한 차이점은 call 문은 end문에 의해서 주 프로그램으로 리턴하지만, jump문은 리턴하지 않는다는 점입니다.

### 사용 예

call문 설명에서 본 예제 프로그램을 jump문으로 바꾸어 실행해 보면 결과는 아래와 같습니다. 서브프로그램\(0102\_err\)의 end를 만났을 때, 동작 사이클이 종료됩니다. 다음 동작 사이클을 수행하면, 주 프로그램\(0001\)의 처음부터 수행됩니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>print &quot;main job start&quot;
          <br />
        </p>
        <p>jump 102_err
          <br />
        </p>
        <p>print &quot;main job end&quot;
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0102_err.job</td>
      <td style="text-align:left">
        <p>print &quot;sub-program&quot;
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">
        <p>main job start
          <br />
        </p>
        <p>sub-program
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>



