# `_spot_cnd`

### Description

A system variable for reading or changing clearance values for each spot welding condition. <br>
Condition numbers start from 1.

|Member|Meaning|Access|
|:--|:--|:--|
|`fixed_tip_clearance`|Fixed tip clearance|Read/write|
|`moving_tip_clearance`|Moving tip clearance|Read/write|

### Syntax and sample

```python
     var clearance=_spot_cnd[1].fixed_tip_clearance
     _spot_cnd[1].fixed_tip_clearance=clearance
```
