# 입출력 변수

![](../../.gitbook/assets/image%20%281%29.png)

do, dob, dow, dol, dof에서 접미사 b, w, l, f는 각기 byte, word, long, float를 뜻하며 모두부호있는 값\(signed value\)입니다. 이들은 별개의 메모리 공간이 아니라 같은 960 bit의 공간을 서로 다른 데이터형으로 표현한 것입니다. 예를 들어 do\[0~15\]와 dob\[0~1\], dow\[0\]은 모두 동일한 출력신호입니다. 인덱스는 do는 bit단위, dob, dow, dol, dof는 byte단위로 매겨집니다.

![](../../.gitbook/assets/image%20%282%29.png)

do로 시작하는 출력변수에 값을 대입하면, I/O신호 출력이 수행됩니다. 현재, 입력되고 있는 I/O신호값은 di로 시작하는 입력변수값을 읽어 얻을 수 있습니다.

do변수는 읽기, 쓰기가 모두 가능하지만, di변수는 읽기만 가능합니다.



fb 객체명은 아래와 같이 생략할 수도 있습니다.

| \*\*\*\* | **do 표기** | fb.do 표기 |
| :--- | :--- | :--- |
| fb0 | do0 ~ do959 | fb0.do0 ~ fb0.do959 |
| fb1 | do960 ~ do1919 | fb1.do0 ~ fb1.do959 |
| fb2 | do1920 ~ do2879 | fb2.do0 ~ fb2.do959 |
| fb3 | do2880 ~ do3839 | fb3.do0 ~ fb3.do959 |
| fb4 | do3840 ~ do4799 | fb4.do0 ~ fb4.do959 |
| fb5 | do4800 ~ do5759 | fb5.do0 ~ fb5.do959 |
| fb6 | do5760 ~ do6719 | fb6.do0 ~ fb6.do959 |
| fb7 | do6720 ~ do7679 | fb7.do0 ~ fb7.do959 |
| fb8 | do7680 ~ do8639 | fb8.do0 ~ fb8.do959 |
| fb9 | do8640 ~ do9599 | fb9.do0 ~ fb9.do959 |


