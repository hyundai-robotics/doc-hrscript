# 6.5 Sci module : Serial communication

Serial communication can be performed through the COM port of the ${cont_model} controller.

To use this function, you must create a Sci object as a global variable as shown below.

Also, be sure to check the settings specifications in [System > 2. Control Parameters > 3. Serial Port] before use.

```python
global sci2
sci2=com.Sci(2)
```

After creating a Sci object, simply call the send, recv, open, and close member procedures.

When calling send, you must input the string to be sent in advance.

When calling recv, it is assigned to the specified string variable upon successful reception. 

When calling open, the port is opened.

When calling open, the port is closed.




