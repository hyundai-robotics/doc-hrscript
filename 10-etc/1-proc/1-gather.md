# 10.1.1 gather

`gather` is the procedure that specifies the start and end of the gathering when you use the data gathering function.

### Description

Specifies the start and end of gathering with `gather`. The gathering result file is saved as follows;
- Storage path: MAIN/project
- File name: 0001.GDT to 0030.GDT

Up to 30 gathering result files are stored, and if the number is exceeded, the previous collection result file is overwritten.

`gather_state()` function returns the current state of the data collection operation.
  - 0 : not in gathering.
  - 1 : in gathering. (gather 1 ~ gather 0)
  - 2 : saving the gathering results as a file. (gather 0~)

### Syntax

```python
gather <start/end>
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
      <td style="text-align:left">start/end</td>
      <td style="text-align:left">
        <ul>
        <li>1: data gathering start</li>
        <li>0: data gathering end</li>
        </ul>
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
S1   move L,spd=100%,accu=0,tool=0
     gather 1
S2   move L,spd=100%,accu=0,tool=0
     delay 1.5
S3   move L,spd=100%,accu=0,tool=0
     gather 0
     end
```