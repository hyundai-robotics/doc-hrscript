# 9.1.1 mkdir문

mkdir문은 디렉토리를 생성하는 프로시져입니다.

### 설명

MAIN 모듈에 지정한 경로의 디렉토리를 생성합니다.

- 티치펜던트나 USB메모리에는 생성할 수 없습니다.
- 중간 경로의 디렉토리가 존재하지 않으면, 중간 경로까지 만들어줍니다.

### 문법

mkdir &lt;경로&gt;

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
      <td style="text-align:left">경로</td>
      <td style="text-align:left">
        생성할 디렉토리 경로.<br>
        맨 앞에는 /를 붙이지 마십시오.
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
mkdir "work/data1"
```

![](../../_assets/mkdir.png)

