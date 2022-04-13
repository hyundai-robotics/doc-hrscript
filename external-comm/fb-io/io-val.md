# 6.1.1 Input/Output Variables

![](../../_assets/image%20%288%29.png)

In do, dob, dow, dol, and dof, the suffixes b, w, l, and f mean “byte,” “word,” “long,” and “float,” respectively, and all are signed values. These are not separate memory spaces and represent the same 960-byte space just with different data types. For example, do\[1~16\], dob\[1~2\], and dow\[1\] are all the same output signals.

![](../../_assets/image%20%282%29.png)

If a value is assigned to an output variable that starts with “do,” I/O signal output will be performed. The I/O signal currently being inputted can be acquired by reading the input variable value that starts with “di.” The do variable can be read and written, but the di variable can only be read.



The FB object name can be omitted as follows.

| **object name** | **do notation** | fb.do notation |
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



