# 3.7.1 call문

### 설명

HRScript에서 메인 프로그램\(main program\)과 서브 프로그램\(sub program\) 간의 형식 상의 큰 차이는 없습니다. 기동 버튼이나 신호로 처음 실행된 JOB은 주 프로그램이고, call 명령문에 의해 호출된 JOB은 모두 서브 프로그램입니다. 

### 문법

```python
call <JOB번호 혹은 파일이름> [,매개변수1,매개변수2,…]
```

call 뒤에 JOB 번호, 혹은 JOB파일이름\(확장자 제외\)을 지정합니다. A라는 프로그램이 수행되다가 call B를 만나면 A의 수행은 중단되고, 서브프로그램인 B 프로그램의 첫 명령문부터 수행이 계속됩니다. B 수행 중 end문이나 return 문을 만나면 호출했던 A 프로그램 call문의 다음 명령문 위치로 복귀하여 A의 수행을 계속하게 됩니다.

### 사용 예

아래는 call 문에 의한 서브프로그램 호출의 예와 그 결과입니다. 서브프로그램이 하는 일이 print문 1개 뿐이라 프로그램을 둘로 분리한 것이 의미없어 보이기는 하지만 뒤에서 좀 더 실제적인 예를 보이도록 하겠습니다.

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
        <p>call 102_err
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
        <p>main job end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

