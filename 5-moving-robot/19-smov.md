# 5.19 smov문

smov문은 포지셔너 동기 시 사용되는 프로시져입니다.
smov문에 대한 자세한 설명은 아래 링크를 참조하십시오.  
[Hi6 로봇제어기 기능설명서 - 포지셔너 동기](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/korean/README)
<br><br>

### 문법
```python
"smov S<스테이션 번호>,<보간방식>,tg=<목표위치>,spd=<속도>,accu=<Accuracy>,tool=<Tool 번호>",
"smov S<스테이션 번호>,<보간방식>,tg=<목표위치>,spd=<속도>,accu=<Accuracy>,tool=<Tool 번호> until <입력신호>"
```