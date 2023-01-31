# LILIN-Edge-AI-ToF-Camera
LILIN IP ToF cameras are high performance Sony 3D DepthSense ToF sensor. The Indirect Time-of-Flight (ToF) technology can measure AI object’s ranged from 0.3-meter to 7-meter, millimeter grade. The ToF camera has 4 x 940nm VCSELs that can work indoor and outdoor under sunlight.  The camera is also an IP67 ratio for outdoor environment.

LILIN IP ToF Cameras adopt the latest H.265 compression technologies, which allow multiple streaming of H.264/H.265 formats in 640 x 480 resolutions for the 2D depth color image. LILIN’s multiple streaming technology transmits digital video at various bit rates and frame rates to suit both high and low bandwidth network environments.

LILIN IP cameras provide various alarm notifications including mobile device live access, email notification with JPEG snapshots, HTTP push notification, and JPEG-to-FTP upload.

The combination of LILIN Navigator software and IP cameras will maximize your system performance and deliver an integrated system solution for your migration to IP videos.

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

#  Get recognition results
Get run-time recognition results.  Both HTTP based and websocket are supported.
```
Syntax: 
http://<serverIP:8592>/getalarmmotion
```

```
Syntax: 
ws://<serverIP:8592>/getalarmmotion
```
	
```
--myboundary
\r\n
Content-Length: <CLength>
\r\n
Content-Type: text/html; charset=utf-8
\r\n
\r\n
CamTime: <TimeStamp>\r\n
{
"AiEngine":<JSON>
}
--myboundary
\r\n
Content-Length: <CLength>
\r\n
Content-Type: text/html; charset=utf-8
\r\n
\r\n
CamTime: <TimeStamp>\r\n
{
"AiEngine":<JSON>
}
```

| Parameter	| Value  | Description | 
| --- |  --- |  --- | 
| CLength	| Integer| HTTP content length| 
| TimeStamp	| String | Date & time info, eg. 2019-09-27 00:53:48| 
| id | Integer | The object sequence of a frame |
| channel_id | Integer | The channel ID, fix to 1 if it is an IP camera |
| camera_name | String | The name of the camera |
| res_height | Integer | The canvas resolution in height of the bounding box drawing even the AI is in 4K recognition. |
| res_width | Integer | The canvas resolution in width of the bounding box drawing even the AI is in 4K recognition. |
| confidence | Integer | The confidence threshold of zone #1 |
| confidence | Integer | The confidence threshold of zone #1 |
| confidence2 | Integer | Reserve for future use |
| progress_bar | Integer | The setting writing progress when apply back to the camaera. |
| engine_type | Integer | The license type of the license key |
| label_name | String | The classified object name |
| class_id | Integer | The classified object ID |
| obj_type | String | Reserve for future use |
| obj_tracking_id | Integer | The tracking ID of a classified object |
| obj_dwell_time | Integer | The tracked object's time in second |
| color_id | Integer | The color ID, see [color table](https://github.com/LILINOpenGitHub/LILIN-Edge-Aida-Camera/blob/main/Color%20ID/ColorID.json) |
| color | String | The name of the color |
| linked_plate | String | The number plate is linked to an object |
| x | Integer | The x position of an object relative to res_height and res_width |
| y | Integer | The y position of an object relative to res_height and res_width |
| w | Integer | The width of an object relative to res_height and res_width |
| h | Integer | The width of an object relative to res_height and res_width |
| parent_idx | Integer | The object belong to a parent, used by linked_plate |
| detection_zone_id | Integer | zone # 1 ~ 4 |
| behavior_id | Integer | The behavior ID of an object in a zone, see [behavior table](https://github.com/LILINOpenGitHub/LILIN-Edge-Aida-Camera/blob/main/behaviorID/behaviorID.json) |

Example: <BR>
{"AiEngine":[],"counter_count":[0,0,0,0,0,0,0,0],"something_vanish_in_zone1":"No","something_vanish_in_zone2":"No","something_vanish_in_zone3":"No","something_vanish_in_zone4":"No","Count":0,"configdirty":0,"AI_fps":10,"red_light":0,"snap_size":0,"snap_response":"Disable","snap_image":"","AIToF":{"Time":"1675132307","global_min":"0.000000","global_min_x":"0","global_min_y":"0","global_max":"7.400000","global_max_x":"0","global_max_y":"0","unit":"m"}}

| Parameter	| Value  | Description | 
| --- |  --- |  --- | 
|global_min | | The global depth of the tof in meter|
|global_max | | The global depth of the tof in meter|
|global_min_x | | The point cloud X of the global min |
|global_min_y | | The point cloud Y of the global min |
|global_max_x | | The point cloud X of the global max |
|global_max_y | | The point cloud Y of the global min |
	
	


