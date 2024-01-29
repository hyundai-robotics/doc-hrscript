# 10.1.13 task문

task문은 멀티태스크 기능을 수행하는 프로시져입니다.
task문에 대한 자세한 설명은 아래 링크를 참조하십시오.  
[Hi6 로봇제어기 기능설명서 - 멀티태스킹](https://hrbook-hrc.web.app/#/view/doc-multi-task/korean/README)
<br><br>

### 문법

```python
task start,sub=<서브태스크 번호>,job=<프로그램 번호>
task wait,sub=<서브태스크 번호>
task sync,id=<식별자>,no=<동일 id의 실행 갯수>
task stop,sub=<서브태스크 번호>
task reset,sub=<서브태스크 번호>
```