# 5.18 axisctrl 문


## 설명 
* axisctrl 명령어는 move 명령어 실행에 의해 각 축의 위치를 이동할 때, 부가축에 대해 목표위치로 이동할지 여부를 지정하는 기능입니다.  
* axisctrl문에 대한 자세한 설명은 아래 링크를 참조하십시오.  
[Hi6 로봇제어기 기능설명서 - 멀티태스킹](https://hrbook-hrc.web.app/#/view/doc-multi-task/korean/README)

## 문법 
```python
axisctrl <on/off>,a=<부가축 번호>
axisctrl <on/off>,a=[부가축 번호,부가축 번호,...] : 복수지정 가능(최대 4개)
```