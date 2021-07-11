# 문자열 자료형

앞 절의 첫 프로그램에서 print 문의 파라미터로서 "Hello, World" 라는 데이터를 사용했는데 이것은 문자열 자료형입니다. 문자열 자료형의 값은 큰 따옴표로 시작하고 끝납니다. 문자열 길이의 제한은 없습니다.

```javascript
print "Welcome to the Robot World."
```

문자열 내의 따옴표 혹은 특수 문자를 표현하기 위해 역슬래시\(\\)로 시작하는 시퀀스가 사용됩니다. 이러한 시퀀스를 이스케이프\(escape\) 문자라고 합니다.

지원되는 이스케이프 문자는 아래 표와 같습니다.

| \" | 큰 따옴표 \(double quote\) |
| :--- | :--- |
| \\ | 역 슬래시 \(backslash\) |
| \t | 탭 \(tab\) |
| \n | 개행 문자 |

```javascript
print "Message:\nPlease, press \"OK\" button."

출력결과
Message:
Please, press "OK" button.
```



