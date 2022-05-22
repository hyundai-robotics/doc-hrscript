# 3.1 주소 \(Address\)

순서대로 다음 행을 수행하지 않고 프로그램의 다른 위치로 이동하는 것을 분기\(branch\)라고 합니다. 주소란 분기의 목적지\(destination\) 입니다.주소를 정의하는 방법은 행번호와 레이블의 2가지입니다. 아래의 예에서 두 번째 명령문의10은 행번호이고, 마지막 명령문 \*err\_handle은 레이블입니다.

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
10   z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
```



