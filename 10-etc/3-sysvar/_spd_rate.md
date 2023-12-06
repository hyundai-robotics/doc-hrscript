# _spd_rate

Get or set the playback speed-rate.

### Description

Same setting as cond.set - Playback speed rate.

- unit : %
- range : 1 to 100
- default value : 100

### Syntax

```python
var res
res = _spd_rate
```

### Sample

```python
   ...
   # If playback speed is less than 50%, raise it to 100%.
   if _spd_rate<50
     _spd_rate=100
   ...
   end
```
