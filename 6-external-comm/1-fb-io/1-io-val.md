# 6.1.1 Input/Output Variables

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table>
<thead>
  <tr>
    <td colspan="3"></td>
    <td>Type</td>
    <td>Value range</td>
  </tr>
</thead>
<tbody> 
  <tr>
    <td rowspan="10">fb0 ~ fb9</td>
    <td rowspan="5">Digital output</td>
    <td>do[0~959] <br>
    dob[0~119].x[0~7] <br>
    dow[0~118].x[0~15] <br>
    dol[0~116].x[0~31] </td>
    <td>bit</td>
    <td>0, 1</td>
  </tr>
  <tr>
    <td>dob[0~119]</td>
    <td>signed 1byte integer</td>
    <td>-128 ~ +127</td>
  </tr>
  <tr>
    <td>dow[0~118]</td>
    <td>signed 2byte integer</td>
    <td>-32768 ~ +32767</td>
  </tr>
  <tr>
    <td>dol[0~116]</td>
    <td>signed 4byte integer</td>
    <td>-2147483648 ~ +2147483647</td>
  </tr>
  <tr>
    <td>dof[0~116]</td>
    <td>signed 4byte real number</td>
    <td>3.4E+/-38 (7 significant figures)</td>
  </tr>
  <tr>
    <td rowspan="5">Digital input</td>
    <td>di[0~959] <br>
    dob[0~119].x[0~7] <br>
    dow[0~118].x[0~15] <br>
    dol[0~116].x[0~31] </td>
    <td>bit</td>
    <td>0, 1</td>
  </tr>
  <tr>
    <td>dib[0~119]</td>
    <td>signed 1byte integer</td>
    <td>-128 ~ +127</td>
  </tr>
  <tr>
    <td>diw[0~118]</td>
    <td>signed 2byte integer</td>
    <td>-32768 ~ +32767</td>
  </tr>
  <tr>
    <td>dil[0~116]</td>
    <td>signed 4byte integer</td>
    <td>-2147483648 ~ +2147483647</td>
  </tr>
  <tr>
    <td>dif[0~116]</td>
    <td>signed 4byte real number</td>
    <td>3.4E+/-38 (7 significant figures)</td>
  </tr>
</tbody>
</table>

<br><br>

In do, dob, dow, dol, and dof, the suffixes b, w, l, and f mean “byte,” “word,” “long,” and “float,” respectively, and all are signed values. These are not separate memory spaces and represent the same 960-byte space just with different data types. For example, do\[1~16\], dob\[1~2\], and dow\[1\] are all the same output signals.

![](../../_assets/image_2.png)

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



