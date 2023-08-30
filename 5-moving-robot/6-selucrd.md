# 5.6 selucrd - select user coordinate system

The selucrd statement is a procedure for changing the user coordinate system number specified as the user coordinate system in the condition setting.

### Description

Function corresponding to specifying the User coordinate system in the condition setting.

### Syntax

```python
selucrd <coord. system number>
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
      <td style="text-align:left">coord. system number</td>
      <td style="text-align:left">
        coord. system number to select<br>
        <ul>
        <li>0: Unspecifying user coordinate system</li>
        <li>1~20: Specifying a User Coordinate system</li>
        </ul>
      </td>
      <td style="text-align:left">expression</td>
    </tr>
  </tbody>
</table>

### Example

```python
   selucrd 1
   end
```