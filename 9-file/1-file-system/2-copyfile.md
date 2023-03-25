# 9.1.2 copyfile

A copyfile is a procedure that requests to copy a directory or file.

### Description

Copies a directory or file of specified source path to the specified destination pathname.

- Can only be performed within the MAIN module, not Teach Pendant or USB memory.
- If a directory of the intermediate path of the destination pathname does not exist, it creates the intermediate path.
- If the destination directory already exists, delete it and copy the source directory.
- Overwrite the destination file if it already exists.
- All subdirectories in the directory are also copied.
- The pathname also supports wildcard ('*', '?').

- Because large files or entire directories may be copied, it is asynchronously performed in the background to avoid loss of tact time due to waiting during copying. In other words, when the copyfile statement is performed, starting the copy in the background task, immediately proceed with the next statement. For example, you can request a copy and execute the move statements. The successful completion of the copy can be determined by reading the values of the result-variable. (That is, no errors or warnings are generated when the copy fails.)

- You cannot request another copy or deletion until one copy or deletion is complete.


### Syntax

```python
copyfile <result-variable>,<source pathname>,<destination pathname>
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
        <li>0: Copy in progress.</li>
        <li>-1: Source pathname is invalid.</li>
        <li>-2: Destination pathname is invalid.</li>
        <li>-3: Failed to copy.</li>
        <li>-6: All failed when copying wildcard.</li>
        <li>-7: Some failed when copying wildcard.</li>
        <li>-11: Failed to create temporary path.</li>
        <li>-12: Failed to copy to temporary path.</li>
        <li>-13: Failed to clear existing destination path.</li>
        <li>-14: Destination path creation failed.</li>
        <li>-15: Move from temporary path to destination path failed.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">source pathname</td>
      <td style="text-align:left">
        directory's path to copy,<br>
        or file's pathname to copy
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
    <tr>
      <td style="text-align:left">string expression</td>
      <td style="text-align:left">
        - End with '/': Path to be copied.<br>
        - Not end with '/': Pathname that will be created by copying.
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   var res
   copyfile res,"project/vars","work/vars_1" # vars_1/ folder is created.
   wait res==1,8,*timeout
   copyfile res,"project/vars","work/vars_1/" # vars_1/vars/ folder is created.
   wait res==1,8,*timeout
   copyfile res,"work/clear.job","project/jobs/0005_clear.job"
   wait res==1,4,*timeout
   copyfile res,"work/*_sub.job","project/jobs/" # wildcard
   wait res==1,4,*timeout
   call 5
   end
   *timeout
   print "copyfile failed"
   end
```

![](../../_assets/copyfile.png)

