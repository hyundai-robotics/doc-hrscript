# 9.1.3 delfile

A delfile is a procedure that requests to delete a directory or file.

### Description

Deletes a directory or file in the specified path.

- Can only be performed within the MAIN module, not Teach Pendant or USB memory.
- All subdirectories in the directory are also deleted.
- If the specified pathname does not exist, it ends with success.
- wildcard is not supported.

- Because large files or entire directories may be deleted, it is asynchronously performed in the background to avoid loss of tact time due to waiting during deletion. The successful completion of the deletion can be determined by reading the values of the result-variable.

- You cannot request another copy or deletion until one copy or deletion is complete.


### Syntax

```python
delfile <result-variable>,<pathname>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        result of background execution<br>
        <ul>
        <li>1: Successfully completed.</li>
        <li>0: Deletion in progress.</li>
        <li>-1: Failed to delete directory.</li>
        <li>-11: Failed to delete file.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">pathname</td>
      <td style="text-align:left">
        directory's path to delete,<br>
        or file's pathname to delete
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   var res
   delfile res,"work/vars_1"
   wait res==1,8,*timeout
   copyfile res,"project/jobs/0005_sub.job"
   wait res==1,4,*timeout
   end
   *timeout
   print "delfile failed"
   end
```
