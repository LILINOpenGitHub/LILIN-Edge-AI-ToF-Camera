# LILIN-Edge-AI-ToF-Camera
LILIN DS632 ToF camera is a IP based PoE ToF camera for 3D structure light.
![image](https://github.com/LILINOpenGitHub/LILIN-Edge-AI-ToF-Camera/blob/main/image/ds632.jpg)

## The SDK
```
Syntax:
http://192.168.0.200:8592/gettofrange
```
Return:
{
"min_tof_range":"0.000000", 
"max_tof_range":"7.400000", 
"unit":"M"
}

```
Syntax:
http://192.168.50.200:8592/gettofpixel?x=<myX>&y=<myY>&angle=<myAngle>
```
Return:
{
"x":"1", 
"y":"1", 
"depth":"0.000000"
}

Parameters
| Parameters	|  Description 	|	 
| ---  		|  ---  	|  
| myX   		| X axis 		| 
| myY 		| Y axis 	| 
| myAngle 		| The angle   	| 
