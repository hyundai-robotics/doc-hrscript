# 9.2.1 load_job

Statement that reads changes of the MAIN module's project/jobs/ folder to update the memory.


### Description

Load the jobs in the project/jobs/ folder of the MAIN module into new memory.

If you copy or overwrite .job files into the jobs/ folder with FTP or copyfile commands, you must perform this statement to reflect the memory to be able to select or call the job.

- CAUTION: Jobs in memory that do not exist in the jobs/ folder will be deleted.
- If the file has different modified time, it is loaded.
- Files that do not exist in memory are loaded.

- Since large capacity .jobs can be loaded, it is performed asynchronously in the background to avoid loss of tact time due to load. The successful completion of the load can be determined by reading the values of the resulting variables.
- You cannot request another load until the load is finished.



### Syntax

```python
load_job <result-variable>,"*"
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
        <li>0: Load in progress.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">job filename</td>
      <td style="text-align:left">
        You can only use the "*" argument, which means all files.
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var res
     copyfile res,"project/vars","work/vars_1"
     wait res==1,8,*timeout
     copyfile res,"work/sub5.job","project/jobs/0005_sub.job"
     wait res==1,4,*timeout
     load_job res,"*"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "copyfile failed"
     end
```
