# 2.3.1 프로시져

프로시져는 명령어와 0~N개의 매개변수\(parameter\)들로 구성됩니다.

```python
move P,po3,spd=80%,accu=1,tool=3 until do33
```

프로시져 매개변수는 아래와 같이 3가지 종류가 있습니다.

| 종류 | 문법 | 예제 |
| :--- | :--- | :--- |
| 위치\(position\) 매개변수 | &lt;value&gt; | P, po3 |
| 키워드\(keyword\) 매개변수 | &lt;keyword&gt;=&lt;value&gt; | spd=80%, accu=1, tool=3 |
| 전치사\(preposition\) 매개변수 | &lt;preposition&gt; &lt;value&gt; | until do33 |

위치매개변수는 몇 번째에 위치하는지에 따라 그 역할이 결정되므로, 위치가 바뀌어서는 안 되며, 프로시져의 가장 앞 부분에 있어야 합니다. 키워드 매개변수는 위치매개변수 다음에 있어야 하지만, 키워드 매개변수들 간의 순서는 동작에 영향을 주지 않습니다.

전치사 매개변수는 맨 마지막에 배치됩니다.



