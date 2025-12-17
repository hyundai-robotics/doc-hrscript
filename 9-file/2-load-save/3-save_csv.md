# 9.2.3 save_csv

Supported from V60.28-00.

Statement that stores the global root array variable in memory as a .csv file in the `project/vars/` folder of the MAIN module.

### Description

The global root array of HRScript is stored in the `vars/` folder as a file in CSV standard format. ('Root' means that it is not a property of another array or object.)

For information on variable files, please refer to the operation manual link below.

[global variable/variable file](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/english-${cont_model}-tp630/6-monitoring/3-job/3-global-variable/3-var-files)

The global root arrays are not immediately stored to the .csv file whenever the value changes.
It is saved as a file when you press `Ctrl+[F7: save]` or power off, and you can save it as a file immediately by executing the `save_csv` command.

- Because large .csv's can be saved, they are performed asynchronously in the background to avoid loss of tact time due to saving. The successful saving can be determined by reading the value of the result-variable.
- You cannot request another saving until current saving is finished.


### Syntax

```python
save_csv <result-variable>,"*"
save_csv <result-variable>,"<variable name>"
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
        <li>1: Completed.</li>
        <li>0: Save in progress.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">.csv file title</td>
      <td style="text-align:left">
        <ul>
        <li>"*": saves all variable.</li>
        <li>"&lt;variable name&gt;": Saves &lt;variable name&gt;.csv file.</li>
        </ul>
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
If you save all .csv by specifying "*", it does not delete the .csv files in the `vars/` folder because the root variable of the corresponding name does not exist.
{% endhint %}

### Sample

```python
     var res
     save_csv res,"locs"
     wait res==1,4,*timeout
     copyfile res,"project/vars/locs.csv","work/arrs/locs2.csv"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "failed to save new locations."
     end
```
