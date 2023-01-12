# LILIN-Edge-AI-ToF-Camera
LILIN DS632 ToF camera is a IP based PoE ToF camera for 3D structure light.
![image](https://github.com/LILINOpenGitHub/LILIN-Edge-AI-ToF-Camera/blob/main/image/ds632.jpg)

## The SDK

## Get minimum and maximun hight/depth values for the ToF Camera
```
Syntax:
http://192.168.0.200:8592/gettofrange
```
<strong>Return: </strong> <BR>
{ <BR>
"min_tof_range":"0.000000",  <BR>
"max_tof_range":"7.400000", <BR>
"unit":"M" <BR>
} <BR>

Parameters
| Parameters	|  Description 	|	 
| ---  		|  ---  	|  
| min_tof_range   		| The minimun hight or depth of ToF in meter		| 
| max_tof_range 		| The maximun hight or depth of ToF in meter | 
| unit 		| The unit of the ToF in meter or foot 	| 
  
## Get hight/depth by a X and Y on the screen
```
Syntax:
http://192.168.0.200:8592/gettofpixel?x=<myX>&y=<myY>
```
<strong>Return: </strong> <BR>
{ <BR>
"x":"1",  <BR>
"y":"1",  <BR>
"depth":"5.03" <BR>
"height": "2.03" <BR>
"distance": "3.15" <BR>
} <BR>

Parameters
| Parameters	|  Description 	|	 
| ---  		|  ---  	|  
| myX   		| X axis = 0 ~ 799		| 
| myY 		| Y axis = 0 ~ 599	| 
| myAngle 		| The angle = 90, 60, 45, 30, or 0  	| 
