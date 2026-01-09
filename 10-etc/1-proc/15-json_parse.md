# 10.1.15 json_parse문

V60.32-00 부터 지원 됩니다.

json 문자열을 파싱하여 객체, 배열, 값으로 변경 하기 위한 프로시져 입니다.

### 문법

프로시져 시작 직후 `result()` 함수를 사용하여 결과 데이터가 저장될 객체를 받습니다.
```python
    json_parse <json string literal/value>
    var r = result()
```

파싱 완료 대기
```python
    wait r.status == "finished"
```

이후 r.data에 json 문자열을 파싱한 결과가 저장 되어 있음. 대기 없이 r.data를 사용하면 파싱이 완료 되지 않은 경우 에러 발생 할 수 있음.


##### status

<table>
  <thread>
    <th style="text-align:left">status</th>
    <th style="text-align:left">상세 내용</th>
  </thread>
  <tbody>
  <tr>
    <td style="text-align:left">parsing</td>
    <td style="text-align:left">json 파싱이 진행 중. data를 사용 할 수 없음.</td>
  </tr>
  <tr>
    <td style="text-align:left">finished</td>
    <td style="text-align:left">json 파싱이 완료 됨. data를 사용 할 수 있음</td>
  </tr>
  </tbody>
</table>



### 사용 예
```python
    json_parse "[1, 2, 3, 4]"
    var r = result()
    wait r.status == "finished", 10 # 최대 10초간 파싱 완료 대기
    var jr = r.data   # r.data의 타입은 array
    print jr          # [1, 2, 3, 4] 출력 됨
```

```python
    json_parse "3.141592"
    var r = result()
    wait r.status == "finished", 10 # 최대 10초간 파싱 완료 대기
    var jr = r.data    # r.data의 타입은 double
    print jr           # 3.141592 출력 됨
```
```python
    json_parse "{\"test\": \"value\"}" # 사용되는 따옴표는 escape 되어야 함
    var r = result()
    wait r.status == "finished", 10 # 최대 10초간 파싱 완료 대기
    var jr = r.data    # r.data의 타입은 JObject
    print jr           # { _type: "JObject", _sub_file: "", _desc: "", test: "value" } 출력 됨
```
