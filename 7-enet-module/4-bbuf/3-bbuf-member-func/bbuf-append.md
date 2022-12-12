# append

### Description

Appends data in the specified format to a binary buffer.


### Syntax

`{BBuf object}.append {format},{data}`


### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Misc.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">format</td>
      <td style="text-align:left">binary format<sup>*</sup><br>
      e.g. "U4", "s2"
      </td>
      <td style="text-align:left">string</td>
    </tr>
	 <tr>
      <td style="text-align:left">data</td>
      <td style="text-align:left">
        data to append in binary buffer
      </td>
      <td style="text-align:left">primitive data,<br>or 1-D array of primitive data</td>
    </tr>
  </tbody>
</table>

<br>


* See [7.4.2 Supported format](../2-format.md).
* If data of a different type from the specified format, automatic type casting is performed implicitly. For example, if the format is "s2" (2-byte integer) and the data is a float value of 3.7, the integer value 3(0x0003) is appended to the buffer.
Conversely, if format is "f4" (4-byte real number) and data is an integer value of -3, the real value -3.0(0xC0400000) is stored in the buffer.
* If the format is unsigned and the data is a negative number, an error occurs, so be careful.

<br>


### Return value

The number of data appended.


### Example

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
```
