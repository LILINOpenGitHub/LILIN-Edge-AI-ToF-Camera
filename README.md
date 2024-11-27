# LILIN-Edge-AI-ToF-Camera
LILIN IP ToF cameras are high performance Sony 3D DepthSense ToF sensor. The Indirect Time-of-Flight (ToF) technology can measure AI object’s ranged from 0.3-meter to 7-meter, millimeter grade. The ToF camera has 4 x 940nm VCSELs that can work indoor and outdoor under sunlight.  The camera is also an IP67 ratio for outdoor environment.

LILIN IP ToF Cameras adopt the latest H.265 compression technologies, which allow multiple streaming of H.264/H.265 formats in 640 x 480 resolutions for the 2D depth color image. LILIN’s multiple streaming technology transmits digital video at various bit rates and frame rates to suit both high and low bandwidth network environments.

LILIN IP cameras provide various alarm notifications including mobile device live access, email notification with JPEG snapshots, HTTP push notification, and JPEG-to-FTP upload.

The combination of LILIN Navigator software and IP cameras will maximize your system performance and deliver an integrated system solution for your migration to IP videos.

![image](https://github.com/LILINOpenGitHub/LILIN-Edge-AI-ToF-Camera/blob/main/image/ds632.jpg)
<p>
Visit the video at (https://www.youtube.com/watch?v=H36yX3Axwhw)
</p>

## The SDK

### Query server status
Get the engine status including system ID, version, license and mode info.

#### Syntax
```
http://<serverIP:8592>/server
```
```bash
curl -u <username>:<password> \
    "http://<serverIP:8592>/server"
```
#### Response Parameters
| Parameters      | Type   | Description                                             |
| ---             | ---    | ---                                                     |
| `DeviceName`    | string | Engine name.                                            |
| `Version`       | string | The version number of plugin.                           |
| `Language`      | string | The language setting of plugin.                         |
| `SystemID`      | string | The MAC address of device.                              |
| `LicenseType`   | string | The license type of plugin.                             |
| `LicenseStatus` | string | License status description, showing the remaining days. |
| `UnlockingKey`  | string | The unlocking key of current license.                   |
| `ModeName`      | string | Plugin mode definition, TOF is defined as mod011.        |
#### Response Example
```
DeviceName=GYNet
Version=2.0.5.30-90 Language=en_gb
SystemID=00-0F-FC-74-48-95
LicenseType= EDGETOF (ToF Recognition),
LicenseStatus=Licensed(3 days left)
UnlockingKey=RXYlyY/7r76Ctsc/BI+hbU/z6cHmSy6EgVUvQlMoYwkg1vpYyCTnFpqlJ6rPW7to2qJO9iyPnsQF22kaI4HpvV/Ii1jAvsLFjr2Qr0CSvHE=
ModeName=mod011
```

### Get minimum and maximun depth values of ToF Camera
This API is used to obtain the farthest and nearest depths within the current ToF device field of view, with the distance unit meters.
#### Syntax
```
http://<serverIP:8592>/gettofrange
```
```bash
curl -u <username>:<password> \
    "http://<serverIP:8592>/gettofrange"
```
#### Response Parameters
| Parameters      | Type                    | Description                              |
| ---             | ---                     | ---                                      |
| `min_tof_range` | string ( float format ) | The minimum depth of ToF field of view.  |
| `max_tof_range` | string ( float format ) | The maximun depth of ToF field of view.  |
| `unit`          | string                  | Depth distance unit of ToF. ( M: Meter ) |

#### Response Example
```json
{
    "min_tof_range":"0.000000",
    "max_tof_range":"7.400000",
    "unit":"M"
}
```

  
### Get 3D information by 2D coordinate on the screen
This API can retrieve 3D information for specific 2D coordinates on the screen, including depth, distance, height, and world coordinates. 

The origin of the world coordinate system is based on the point directly below the camera on the ground. The distance unit of this coordinate system is Meter.
#### Syntax
```
http://<serverIP:8592>/gettofpixel?x=<myX>&y=<myY>
```
```bash
curl -u <username>:<password> \
    http://<serverIP:8592>/gettofpixel?x=13&y=25
```
#### Request Parameters
| Parameters | Type | Required | Description                                   |
| ---        | ---  | ---      | ---  	                                       |
| `x`        | int  | Yes      | Coordinate on the X-axis. ( Range : 0 ~ 799 ) |
| `y`        | int  | Yes      | Coordinate on the Y-axis. ( Range : 0 ~ 599 ) | 
#### Response Parameters
| Parameters | Type                    | Description                                                                     |
| ---        | ---                     | ---                                                                             |
| `x`        | string ( int format )   | The 2D X-axis parameter coordinate included when sending the request.           |
| `y`        | string ( int format )   | The 2D Y-axis parameter coordinate included when sending the request.           |
| `depth`    | string ( float format ) | 3D depth of the 2D coordinate position on the screen.                           |
| `height`   | string ( float format ) | Vertical height based on the origin for the 3D point corresponding to the 2D screen coordinates. ( Equivalent to the Z-coordinate in the world coordinate system ) |
| `distance` | string ( float format ) | Horizontal distance based on the origin for the 3D point corresponding to the 2D screen coordinates. |
| `worldX`   | string ( float format ) | The X-coordinate of the 3D point corresponding to the 2D screen coordinates. |
| `worldY`   | string ( float format ) | The Y-coordinate of the 3D point corresponding to the 2D screen coordinates. |
#### Response Example
```json
{
    "x":"13", 
    "y":"25", 
    "depth":"3.458000", 
    "height":"1.668040", 
    "distance":"3.457612", 
    "worldX":"-1.725277", 
    "worldY":"2.996414"
}
```

###  Get recognition results
This API can obtain runtime AI recognition and behavior determination results, including information on objects, zone settings, and behaviors.

Both HTTP based and websocket are supported.

#### Syntax
```bash
http://<serverIP:8592>/getalarmmotion
# Recommended to open with Firefox browser
```
```
ws://<serverIP:8592>/getalarmmotion
```
```bash
curl --verbose --get --http0.9 --user <username>:<password> \
    http://<serverIP:8592>/getalarmmotion
```

The Response data can be broadly divided into two sections: AiEngine and AIToF. 

The following parameters are explained in two corresponding fields.

#### Response Parameters

##### Raw data
| Parameter	        | Type    | Description                                                          |
| ---               | ---     | ---                                                                  |
| `CLength`	        | integer | HTTP content length.                                                 |
| `TimeStamp`	    | string  | Date & time info, eg. 2019-09-27 00:53:48.                           |

##### AiEngine
| Parameter	          | Type    | Description                                                          |
| ---                 | ---     | ---                                                                  |
| `id`                | integer | The object sequence of a frame.                                      |
| `camera_name`       | string  | The name of the camera.                                              |
| `res_height`        | integer | The height of the 2D coordinate system in the AI tracking algorithm. |
| `res_width`         | integer | The width of the 2D coordinate system in the AI tracking algorithm.  |
| `confidence`        | integer | The confidence threshold of zone #N.                                 |
| `label_name`        | string  | The classified object name.                                          |
| `class_id`          | integer | The classified object ID.                                            |
| `obj_tracking_id`   | integer | The tracking ID of a classified object.                              |
| `obj_dwell_time`    | integer | The tracked object's time in second.                                 |
| `x`                 | integer | The x position of an object relative to res_height and res_width.    |
| `y`                 | integer | The y position of an object relative to res_height and res_width.    |
| `w`                 | integer | The width of an object relative to res_height and res_width.         |
| `h`                 | integer | The width of an object relative to res_height and res_width.         |
| `detection_zone_id` | integer | Zone index # 1 ~ 8.                                                  |
| `behavior_id`       | integer | The behavior ID of an object in a zone, please refer to: [behavior table](https://github.com/LILINOpenGitHub/LILIN-Edge-Aida-Camera/blob/main/behaviorID/behaviorID.json) |

Descriptions of irrelevant, under-development, or deprecated parameters are omitted.

##### AIToF

<!-- min_tof_range, max_tof_range -->

| Parameter	      | Type                      | Description                                                                                | 
| ---             | ---                       | ---                                                                                        | 
| `min_tof_range` | string ( float format )   | The minimum depth of ToF field of view.                                                    |
| `max_tof_range` | string ( float format )   | The maximun depth of ToF field of view.                                                    |
| `global_min_x`  | string ( integer format ) | The minimum depth position corresponds to the 2D X-axis coordinates on the screen.         |
| `global_min_y`  | string ( integer format ) | The minimum depth position corresponds to the 2D Y-axis coordinates on the screen.         |
| `global_max_x`  | string ( integer format ) | The maximun depth position corresponds to the 2D X-axis coordinates on the screen.         |
| `global_max_y`  | string ( integer format ) | The maximun depth position corresponds to the 2D Y-axis coordinates on the screen.         |
| `ground1_Ht`    | string ( float format )   | The height value converted based on the ground reference point #1 as configured in the UI. |
| `ground2_Ht`    | string ( float format )   | The height value converted based on the ground reference point #2 as configured in the UI. |
| `ground3_Ht`    | string ( float format )   | The height value converted based on the ground reference point #3 as configured in the UI. |
| `unit`          | string                    | Units of distance for the maximun and minimum depths and ground point height. (m: meter)   |

Descriptions of irrelevant, under-development, or deprecated parameters are omitted.

#### Response Example
Raw data example
```
--myboundary
\r\n
Content-Type: text/plain
\r\n
Content-Length: <CLength>
\r\n
CamTime: <TimeStamp>
\r\n
\r\n
{"AiEngine":[{"id":0,"channel_id":1,"camera_name":"DS362","res_height":1080,"res_width":1920,"confidence":100,"confidence2":0,"progress_bar":0,"engine_type":4,"label_name":"tof_point","class_id":1000,"obj_type":0,"obj_tracking_id":2179,"obj_dwell_time":5,"tof_distance":0,"tof_height":0,"max_height_x":0,"max_height_y":0,"tof_height_velocity":0,"x":1464,"y":1071,"w":60,"h":45,"center_direction":"","parent_idx":-1,"min_distance":963,"max_distance":0,"min_height":749,"max_height":0,"detection_zone_id":0,"detection_zone_id2":0,"detection_zone_id3":0,"detection_zone_id4":0,"behavior_id":0,"clinical_behavior_z1":"00000","clinical_behavior_z2":"00000","clinical_behavior_z3":"00000","clinical_behavior_z4":"00000"},{"id":1,"channel_id":1,"camera_name":"DS362","res_height":1080,"res_width":1920,"confidence":100,"confidence2":0,"progress_bar":0,"engine_type":4,"label_name":"tof_point","class_id":1000,"obj_type":0,"obj_tracking_id":2178,"obj_dwell_time":19,"tof_distance":0,"tof_height":0,"max_height_x":0,"max_height_y":0,"tof_height_velocity":0,"x":1440,"y":405,"w":60,"h":45,"center_direction":"","parent_idx":-1,"min_distance":0,"max_distance":5156,"min_height":0,"max_height":231,"detection_zone_id":0,"detection_zone_id2":0,"detection_zone_id3":0,"detection_zone_id4":0,"behavior_id":0,"clinical_behavior_z1":"00000","clinical_behavior_z2":"00000","clinical_behavior_z3":"00000","clinical_behavior_z4":"00000"}],"counter_count":[0,0,0,0,0,0,0,0],"counter_reset_value":[0,0,0,0,0,0,0,0],"counter_operand":["NULL","NULL","NULL","NULL","NULL","NULL","NULL","NULL"],"counters":[],"something_vanish_in_zone1":"No","person_inside1":"No","something_vanish_in_zone2":"No","person_inside2":"No","something_vanish_in_zone3":"No","person_inside3":"No","something_vanish_in_zone4":"No","person_inside4":"No","something_vanish_in_zone5":"No","person_inside5":"No","something_vanish_in_zone6":"No","person_inside6":"No","something_vanish_in_zone7":"No","person_inside7":"No","something_vanish_in_zone8":"No","person_inside8":"No","Count":2,"configdirty":0,"AI_fps":9,"snap_size":0,"snap_response":"Disable","snap_image":"","AIToF":{"Time":"1732690423","min_tof_range":"1.367000","global_min_x":"488","global_min_y":"476","max_tof_range":"5.367000","global_max_x":"480","global_max_y":"180","unit":"m","ground1_Ht":"1.69","ground2_Ht":"1.72","ground3_Ht":"1.76","ground1_x":0,"ground1_y":0,"ground2_x":0,"ground2_y":0,"ground3_x":0,"ground3_y":0,"ground2_tilt_angle":0,"ground3_tilt_angle":0,"leaning_angle":0}}
--myboundary
\r\n
Content-Type: text/plain
\r\n
Content-Length: <CLength>
\r\n
CamTime: <TimeStamp>
\r\n
\r\n
{
"AiEngine":<JSON>
}
```

JSON format example
```json
{
  "AiEngine": [
    {
      "id": 0,
      "camera_name": "DS362",
      "res_height": 1080,
      "res_width": 1920,
      "confidence": 91,
      "label_name": "person",
      "class_id": 0,
      "obj_tracking_id": 3176,
      "obj_dwell_time": 25,
      "x": 837,
      "y": 238,
      "w": 478,
      "h": 753,
      "behavior_id": 0
    }
  ],
  "AIToF": {
    "min_tof_range": "1.377000",
    "global_min_x": "480",
    "global_min_y": "476",
    "max_tof_range": "5.406000",
    "global_max_x": "488",
    "global_max_y": "200",
    "unit": "m",
    "ground1_Ht": "1.69",
    "ground2_Ht": "1.72",
    "ground3_Ht": "1.76"
  }
}
```
Irrelevant, under-development, deprecated parameters are omitted.


