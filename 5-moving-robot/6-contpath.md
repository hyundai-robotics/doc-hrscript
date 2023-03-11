# 5.6 contpath

### Description

Select the mode of CONTPATH.

See the link below for the description of CONTPATH.
[Operation Manual: 8.15 R360 Set CONTPATH manually](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/english-tp630/8-r-code/15-r360)

<br><br>


### Syntax

```python
contpath <mode number>
```

### Parameter

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
      <td style="text-align:left">mode number</td>
      <td style="text-align:left">
        0: Discontinuous<br>
        1: Continuous. However, input signal is discontinuous (default)<br>
        2: Continuous. Input signal is also continuous
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Example

```python
contpath 0
contpath 1
contpath 2
```


{% hint style="info" %}

- If the `contpath` statement is not explicitly executed, `contpath 1` is applied by default. Even if specified explicitly, it is initialized to `contpath 1` at the start of the cycle.

- The changed status can be checked by the `CP0` / `CP1` / `CP2` flags on the title bar.

{% endhint %}
