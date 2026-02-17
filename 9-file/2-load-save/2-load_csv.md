# 9.2.2 `load_csv`

Supported from V60.28-00.

Statement that reads to memory the changes to the .csv file (root global array) in the `project/vars/` folder of the MAIN module.

### Description

The global root arrays of HRScript is stored in the `vars/` folder as files in CSV standard format. ('Root' means that it is not a property of another array or object.)

For information on variable files, please refer to the operation manual link below.

[global variable/variable file](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-${cont_model}-tp630/6-monitoring/3-job/3-global-variable/3-var-files)

You can easily edit .csv files with a text editor on your PC.
The edited file copied to the `vars/` folder is not immediately reflected in memory, but only by using the `[load all]` function in the TeachPendant's global variable window or executing the `load_csv` statement.

- Because large .csv's can be loaded, they are performed asynchronously in the background to avoid loss of tact time due to loading. The successful loading can be determined by reading the value of the result-variable.
- You cannot request another loading until current loading is finished.


### Syntax

```python
load_csv <result-variable>,"*"
load_csv <result-variable>,"<variable name>"
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
        <li>0: Load in progress.</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">.csv file title</td>
      <td style="text-align:left">
        <ul>
        <li>"*": loads all files.</li>
        <li>"&lt;variable name&gt;": Loads &lt;variable name&gt;.csv file.</li>
        </ul>
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
If you load all .csv with "*", the root arrays in memory that does not have .csv in the `vars/` folder are deleted.
{% endhint %}

### Sample

```python
     var res
     copyfile res,"work/arrs/locs1.csv","project/vars/locs.csv"
     wait res==1,4,*timeout
     load_csv res,"locs"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "failed to load new locations."
     end
```
