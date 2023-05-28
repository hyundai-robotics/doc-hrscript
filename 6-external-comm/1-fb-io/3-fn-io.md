# 6.1.3 fn객체

fb객체의 특정 영역을 지정하여 fn객체를 정의할 수 있습니다.
Hi6 제어기가 필드버스 master이고, 여러 개의 필드버스 slave장치들이 있을 경우, 각 slave장치의 영역들을 하나씩의 fn객체로 설정해두면, 이 slave들을 직관적으로 다룰 수 있습니다.

![](../../_assets/io/io_fn.png)

fn영역을 설정하는 방법은 아래 링크를 참조하십시오.

[조작설명서: 7.3.2.12 fn 블럭 할당](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/7-setting/3-control-parameter/2-io-signal-setting/12-fn-block)
  
&nbsp;

fn의 문법은 fb와 동일한 형식입니다.
fn 인덱스는 0~63이며, bit 인덱스는 fb와 동일하게 0~959입니다.
즉, 최대 설정 가능한 인덱스는 fn0.do0 ~ fn63.do959 입니다.

미설정된 존재하지 않는 fn객체에 접근하거나, fn의 설정 범위를 초과하는 do/di에 접근 시, 에러가 발생합니다.

아래의 사용 예를 참고하십시오.

```python
fn2.dob3=0b00001111  	# fn2의 3번 바이트출력값을 2진 bit열로 지정
fn[4].dob1=0x0F  	# fn4의 1번 바이트출력값 하위 4비트를 켜고, 상위 4비트를 끈다.
var work_no=fn63.dib3    # fn63의 3번 바이트입력값을 work_no 변수에 대입
if fn5.di43 then *err  	# fn5.di42가 켜지면 *err 레이블로 분기
for idx=21 to 29
  fn3.do[idx]=1  	# fn3의 출력신호 do21 ~ do29를 모두 켠다. 
next
fn2.do3=fn2.do7=fn2.do11=1   # fn2의 3번, 7번, 11번 출력신호를 한꺼번에 켠다.
```
