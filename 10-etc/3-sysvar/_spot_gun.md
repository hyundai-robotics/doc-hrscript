# `_spot_gun`

### Description

A system variable for reading or changing tip wear amounts and the completed weld count for each spot welding gun. <br>
Gun numbers start from 1.

|Member|Meaning|Access|
|:--|:--|:--|
|`fixed_tip_consump`|Fixed tip wear amount|Read/write|
|`moving_tip_consump`|Moving tip wear amount|Read/write|
|`total_tip_consump`|Sum of the fixed tip and moving tip wear amounts|Read-only|
|`weld_count`|Number of completed welds for the gun <br> (Supported from V70.04-03)|Read/write|

### Syntax

```python
     var wear=_spot_gun[1].fixed_tip_consump
     var total_wear=_spot_gun[1].total_tip_consump
     var count=_spot_gun[1].weld_count
     _spot_gun[1].weld_count=0
```

### Behavior of weld_count

- Increments by 1 when welding is determined to be complete for the gun. Tip dressing and servo gun automatic setting operations are not counted.
- The counters for all guns are reset to 0 at the start of a cycle.
- The saved value is restored when the power is turned on again. Restoring power alone does not reset the counter.
