# LILIN-Edge-AI-ToF-Camera
LILIN DS632 ToF camera is a IP based PoE ToF camera for 3D structure light.
![image](https://github.com/LILINOpenGitHub/LILIN-Edge-AI-ToF-Camera/blob/main/image/ds632.jpg)

## The SDK
```
Syntax:
http://192.168.0.200:8592/gettofrange
```
Return: <BR>
{ <BR>
"min_tof_range":"0.000000",  <BR>
"max_tof_range":"7.400000", <BR>
"unit":"M" <BR>
} <BR>

```
Syntax:
http://192.168.0.200:8592/gettofpixel?x=<myX>&y=<myY>&angle=<myAngle>
```
Return: <BR>
{ <BR>
"x":"1",  <BR>
"y":"1",  <BR>
"depth":"0.000000" <BR>
} <BR>

Parameters
| Parameters	|  Description 	|	 
| ---  		|  ---  	|  
| myX   		| X axis 		| 
| myY 		| Y axis 	| 
| myAngle 		| The angle = 90, 60, 45, 30, 0  	| 
