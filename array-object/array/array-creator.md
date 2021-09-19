# 4.1.3 Array Constructor Function

It is difficult to create an array with hundreds of elements with the notation \[ \] alone. Any number of arrays may be created by calling the constructor function. Each element will be initialized to 0.

```python
var name = Array(900)	# creates an array of 900 elements
```

If two or more elements are designated, a multidimensional array can be created. In the following example of a 3-dimensional array, \[4\] is the lowest dimension.

```python
var name = Array(3,2,4)	# [3][2][4] numbers of 3-dimensional arrays are created
# [ [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]] ]
```



