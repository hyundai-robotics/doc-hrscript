# 9.1.1 mkdir

mkdir is the procedure making directory.

### Description

Creates a directory for the specified path in the MAIN module.

- You cannot create a directory on Teach Pendant or USB memory.
- If a directory with an intermediate path does not exist, it creates the intermediate path.

### Syntax

```python
mkdir <path>
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
      <td style="text-align:left">path</td>
      <td style="text-align:left">
        The directory path to create.<br>
        Do not put / at the beginning.
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
mkdir "work/data1"
```

![](../../_assets/mkdir.png)
