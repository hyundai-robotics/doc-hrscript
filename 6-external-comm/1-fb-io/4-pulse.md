# 6.1.4 pulse

`pulse` statement is the procedure for signal output of pulse type.

### Description

After tlag time has elapsed, it is output as many times as cnt in the form of On(High) for ton time and Off(Low) for toff time.


### Syntax

```python
pulse <Signal>,tlag=<Lag time>,ton=<On time>,toff=<Off time>,cnt=<output count>
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
      <td style="text-align:left">Signal</td>
      <td style="text-align:left">
        Output signal name to be output in pulse form<br>
        (Only supports fb.do signals.)
      </td>
      <td style="text-align:left">output signal</td>
    </tr>
    <tr>
      <td style="text-align:left">Lag time</td>
      <td style="text-align:left">
        Time to wait until the pulse signal starts after performing the procedure<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">On time</td>
      <td style="text-align:left">
        Time to output signal in On(High) state<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Off time</td>
      <td style="text-align:left">
        Time to output signal in Off (Low) state<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
    <tr>
      <td style="text-align:left">Number of outputs</td>
      <td style="text-align:left">
        Number of times to repeat pulse cycle
        (0 ~ 1000)
      </td>
      <td style="text-align:left">arithmetic expression</td>
    </tr>
  </tbody>
</table>

### Sample

```python
   pulse do10,tlag=0.0,ton=1.5,toff=0.5,cnt=5
   end
```