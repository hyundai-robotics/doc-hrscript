# 5.5 User Coordinate System \(UCS\)

The user coordinate system is a coordinate system in which the user can set the position and direction.

It is created by calling the constructor function Ucs\( \). 



Function parameters are one pose or three poses. When calling is performed with one pose, the pose’s position and direction will be set as the origin and direction of the coordinate system. When calling is performed with three poses, the coordinate system will be created so that pose1 is positioned on the coordinate system’s origin, pose2 is on the x axis of the coordinate system, and pose3 is positioned on the XY plane of the coordinate system.



```python
var <UCS variable name> = Ucs(pose1)
var <UCS variable name> = Ucs(pose1, pose2, pose3)
```

The mkucs function should be used to register a user coordinate system in the system. The argument is similar to the Ucs constructor, but the user coordinate system number \(one or more\) will be inputted as the first argument.

```python
var res = mkucs(num, pose1)
var res = mkucs(num, pose1, pose2, pose3)
```

0 will be returned if successful. An error code of a negative number will be returned if failed.

