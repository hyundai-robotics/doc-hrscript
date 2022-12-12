# 6.3.1 input

### Description

Use the **input** statement to enter a string as a keystroke of the Teach Pendant and store it in a variable. If not entered by the timeout, proceed to the following statement or branch to the timeout address.

### Syntax

input &lt;variable&gt;\[,&lt;timeout&gt;,&lt;timeout address&gt;\]



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
      <td style="text-align:left">variable</td>
      <td style="text-align:left">
        <p>Variable to receive input. Numbers are also entered as string types. If
          numerical values are required, convert to int( ) or double( ) functions.
          <br
          />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">timeout</td>
      <td style="text-align:left">Maximum time limit</td>
      <td style="text-align:left">0.1~60.0 sec
        <br />
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout address</td>
      <td style="text-align:left">Address to branch when timeout is exceeded</td>
      <td style="text-align:left">address</td>
    </tr>
  </tbody>
</table>

### Example

```python
input work_no
input work_no,10
input work_no,10,*timeout
```

![](../../_assets/image_6.png)



