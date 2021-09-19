# 2.3.1 Procedures

A procedure consists of a command and a 0–N number of parameters.

```python
move P,po3,spd=80%,accu=1,tool=3 until do33
```

The three types of procedure parameters are as follows:

| Type | Syntax | Example |
| :--- | :--- | :--- |
| Position parameter | &lt;value&gt; | P, po3 |
| Keyword parameter | &lt;keyword&gt; = &lt;value&gt; | spd=80%, accu=1, tool=3 |
| Preposition parameter | &lt;preposition&gt;  &lt;value&gt; | until do33 |

The position parameter’s role is determined by its position, so it should not be moved and must always be at the front of the procedure. 

Keyword parameters should be placed after position parameters. However, the order between keyword parameters does not affect the operation.



The preposition parameters are placed last.





