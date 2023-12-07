# 10.2.4 rand

You can generate random numbers using the rand function.

### Description
Depending on the function's arguments, it generates a random real number between 0 and 1 or a random integer number within a specified range.

### Syntax
```python
# random real number between 0 and 1
v0=rand() 
```

```python
# random integer number within a specified range
v1=rand(<minimum value>,<maximum value>) 
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
      <td style="text-align:left">minimum value</td>
      <td style="text-align:left">
        minimum random integer number to generate
      </td>
      <td style="text-align:left">integer constant</td>
    </tr>
    <tr>
      <td style="text-align:left">maximum value</td>
      <td style="text-align:left">
        maximum random integer number to generate
      <td style="text-align:left">integer constant</td>
    </tr>
  </tbody>
</table>

### Sample

```python
     var v0, v1
     var min=1
     var max=100
     v0=rand()          # generate random real number between 0 and 1
     v1=rand(min,max)   # generate random integer number between 1 and 100
     end
```

