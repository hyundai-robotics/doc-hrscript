# 10.2.4 rand 함수

rand 함수를 사용하여 난수를 생성할 수 있습니다.

### 설명
함수의 인수에 따라 0과 1 사이의 실수형 난수 또는 지정한 범위 내의 정수형 난수를 생성합니다.

### 문법
```python
# 0과 1 사이의 실수형 난수 생성
v0=rand() 
```

```python
# 지정한 범위 내의 정수형 난수 생성
v1=rand(<최솟값>,<최댓값>) 
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
      <td style="text-align:left">최솟값</td>
      <td style="text-align:left">
        생성할 난수의 최솟값
      </td>
      <td style="text-align:left">정수형 상수</td>
    </tr>
    <tr>
      <td style="text-align:left">최댓값</td>
      <td style="text-align:left">
        생성할 난수의 최댓값
      <td style="text-align:left">정수형 상수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
     var v0, v1
     var min=1
     var max=100
     v0=rand()          # 0과 1 사이의 실수형 난수 생성
     v1=rand(min,max)   # 1과 100 사이의 정수형 난수 생성
     end
```

