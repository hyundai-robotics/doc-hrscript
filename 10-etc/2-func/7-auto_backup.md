# 10.2.7 `auto_backup`

### Description

Requests an automatic backup of controller data. This function can be used to back up data for analysis based on conditions in the program.

The backup runs asynchronously in a separate thread. This function returns the result of the request without waiting for the backup to finish.

Supported from V70.04-03.

### Syntax

```python
     var backup_result=auto_backup()
```

### Parameters

None.

### Return value

|Value|Meaning|
|:--|:--|
|0|The automatic backup request was accepted. This does not mean that the backup has finished.|
|< 0|The request was not accepted because a backup or restore operation is already in progress.|

### Sample

Execute the following comparison after the last weld in the work section has finished and before the next cycle starts or the counter is reset.

```python
     if (_spot_gun[1].weld_count != 34)
         var backup_result=auto_backup()
         if (backup_result != 0)
             print "Automatic backup request failed: ",backup_result
         endif
     endif
```
