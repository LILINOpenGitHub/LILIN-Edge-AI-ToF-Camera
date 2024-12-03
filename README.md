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


### Query detection zone settings
This API is used to obtain information related to the specified zone index.

#### Syntax
```
http://<serverIP:8592>/getconfig?ch=<ch_id>&detection_zone=<zone_id>
```
```bash
curl -u <username>:<password> \
    "http://<serverIP:8592>/getconfig?ch=1&detection_zone=0"
```
#### Request Parameters
| Parameters | Type     | Required | Description                                             |
| ---        | ---      | ---      | ---  	                                                 |
| `ch_id`    | integer  | Yes      | Channel id is a constant on ToF devices, please use 1.  |
| `zone_id`  | integer  | Yes      | Represents the index of the zone (Range: 0 ~ 7).        |

#### Response Parameters
| Parameters                   | Type    | Description                                                                   |
| ---                          | ---     | ---                                                                           |
| `no_parking_time`            | string ( integer format ) | The dwell time threshold in seconds, used on ToF devices for determining conditions related to Person inside and In-bed detection events. |
| `no_parking_time_in_minute`  | string ( integer format ) | The dwell time threshold in minutes, used on ToF devices for determining conditions related to Person inside and In-bed detection events. |
| `obj_max_proportion_in_zone` | string ( integer format ) | The upper bound of the object area ratio filter threshold, calculated as the object area divided by the screen dimensions. |
| `obj_min_proportion_in_zone` | string ( integer format ) | The upper bound of the object area ratio filter threshold, calculated as the object area divided by the screen dimensions. |
| `trigger_events`             | array   | Covers the existing trigger definitions. For the corresponding relationships on ToF devices, please refer to: [ToF behavior table](https://github.com/LILINOpenGitHub/LILIN-Edge-Aida-Camera/blob/main/behaviorID/ToFbehaviorID.json) |
| `point_number`   | integer | Indicates the number of control points in the Nth detection zone.             |
| `x1`             | integer | Indicates the X-coordinate of the #1 control point of the Nth detection zone. |
| `y1`             | integer | Indicates the Y-coordinate of the #1 control point of the Nth detection zone. |
| `x2`             | integer | Indicates the X-coordinate of the #2 control point of the Nth detection zone. |
| `y2`             | integer | Indicates the Y-coordinate of the #2 control point of the Nth detection zone. |
| `x3`             | integer | Indicates the X-coordinate of the #3 control point of the Nth detection zone. |
| `y3`             | integer | Indicates the Y-coordinate of the #3 control point of the Nth detection zone. |
| `x4`             | integer | Indicates the X-coordinate of the #4 control point of the Nth detection zone. |
| `y4`             | integer | Indicates the Y-coordinate of the #4 control point of the Nth detection zone. |
| `x5`             | integer | Indicates the X-coordinate of the #5 control point of the Nth detection zone. |
| `y5`             | integer | Indicates the Y-coordinate of the #5 control point of the Nth detection zone. |
| `x6`             | integer | Indicates the X-coordinate of the #6 control point of the Nth detection zone. |
| `y6`             | integer | Indicates the Y-coordinate of the #6 control point of the Nth detection zone. |

Descriptions of irrelevant, under-development, or deprecated parameters are omitted.

#### Response Example
```json
{
  "no_parking_time": "5",
  "no_parking_time_in_minute": "0",
  "obj_max_proportion_in_zone": "80",
  "obj_min_proportion_in_zone": "0",
  "trigger_events": [
    {
      "checked": 0,
      "detect_event_id": "0x00000001",
      "detect_event_name": "In-bed",
      "post_event_name": "",
      "counter_name": "",
      "counter_increment": ""
    },
    {
      "checked": 0,
      "detect_event_id": "0x00000004",
      "detect_event_name": "Person inside",
      "post_event_name": "",
      "counter_name": "",
      "counter_increment": ""
    },
    {
      "checked": 0,
      "detect_event_id": "0x00000008",
      "detect_event_name": "Personnel entry count (Zone1) / Personnel exit count (Zone2)",
      "post_event_name": "",
      "counter_name": "",
      "counter_increment": ""
    },
    {
      "checked": 0,
      "detect_event_id": "0x20000000",
      "detect_event_name": "Bed leaving",
      "post_event_name": "",
      "counter_name": "",
      "counter_increment": ""
    },
    {
      "checked": 0,
      "detect_event_id": "0x04000000",
      "detect_event_name": "Wake-up detection",
      "post_event_name": "",
      "counter_name": "",
      "counter_increment": ""
    },
    {
      "checked": 1,
      "detect_event_id": "0x08000000",
      "detect_event_name": "Fall detection",
      "post_event_name": "Camera virtual 1",
      "counter_name": "",
      "counter_increment": ""
    }
  ],
  "point_number": 6,
  "x1": 20,
  "y1": 20,
  "x2": 20,
  "y2": 250,
  "x3": 20,
  "y3": 480,
  "x4": 869,
  "y4": 480,
  "x5": 869,
  "y5": 250,
  "x6": 869,
  "y6": 20
}
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
| Parameters | Type     | Required | Description                                   |
| ---        | ---      | ---      | ---  	                                       |
| `x`        | integer  | Yes      | Coordinate on the X-axis. ( Range : 0 ~ 799 ) |
| `y`        | integer  | Yes      | Coordinate on the Y-axis. ( Range : 0 ~ 599 ) | 
#### Response Parameters
| Parameters | Type                    | Description                                                                     |
| ---        | ---                     | ---                                                                             |
| `x`        | string ( integer format )   | The 2D X-axis parameter coordinate included when sending the request.           |
| `y`        | string ( integer format )   | The 2D Y-axis parameter coordinate included when sending the request.           |
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
curl --verbose --get --http0.9 --user "<username>:<password>" http://<serverIP:8592>/getalarmmotion
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
{"AiEngine":[{"id":0,"channel_id":1,"camera_name":"DS362","res_height":1080,"res_width":1920,"confidence":100,"confidence2":0,"progress_bar":0,"engine_type":4,"label_name":"person","class_id":0,"obj_type":0,"obj_tracking_id":293,"obj_dwell_time":301,"tof_distance":1.3609999418258667,"tof_height":1.3055000305175781,"max_height_x":124,"max_height_y":169,"tof_height_velocity":-0.0018666585674509406,"x":210,"y":370,"w":666,"h":705,"center_direction":"","parent_idx":-1,"min_distance":0,"max_distance":0,"min_height":0,"max_height":0,"detection_zone_id":0,"detection_zone_id2":0,"detection_zone_id3":0,"detection_zone_id4":0,"behavior_id":0},{"id":1,"channel_id":1,"camera_name":"DS362","res_height":1080,"res_width":1920,"confidence":100,"confidence2":0,"progress_bar":0,"engine_type":4,"label_name":"tof_point","class_id":1000,"obj_type":0,"obj_tracking_id":339,"obj_dwell_time":4,"tof_distance":0,"tof_height":0,"max_height_x":0,"max_height_y":0,"tof_height_velocity":0,"x":1512,"y":1071,"w":60,"h":45,"center_direction":"","parent_idx":-1,"min_distance":964,"max_distance":0,"min_height":772,"max_height":0,"detection_zone_id":0,"detection_zone_id2":0,"detection_zone_id3":0,"detection_zone_id4":0,"behavior_id":0},{"id":2,"channel_id":1,"camera_name":"DS362","res_height":1080,"res_width":1920,"confidence":100,"confidence2":0,"progress_bar":0,"engine_type":4,"label_name":"tof_point","class_id":1000,"obj_type":0,"obj_tracking_id":336,"obj_dwell_time":27,"tof_distance":0,"tof_height":0,"max_height_x":0,"max_height_y":0,"tof_height_velocity":0,"x":1416,"y":432,"w":60,"h":45,"center_direction":"","parent_idx":-1,"min_distance":0,"max_distance":5233,"min_height":0,"max_height":115,"detection_zone_id":0,"detection_zone_id2":0,"detection_zone_id3":0,"detection_zone_id4":0,"behavior_id":0}],"counter_count":[0,0,0,0,0,0,0,0],"counter_reset_value":[0,0,0,0,0,0,0,0],"counter_operand":["NULL","NULL","NULL","NULL","NULL","NULL","NULL","NULL"],"counters":[],"Count":3,"configdirty":0,"AI_fps":8,"snap_size":0,"snap_response":"Disable","snap_image":"","AIToF":{"Time":"1733218695","min_tof_range":"1.369000","global_min_x":"500","global_min_y":"476","max_tof_range":"5.481000","global_max_x":"472","global_max_y":"192","unit":"m","ground1_Ht":"1.77","ground2_Ht":"1.71","ground3_Ht":"1.75","ground1_x":425,"ground1_y":264,"ground2_x":344,"ground2_y":330,"ground3_x":382,"ground3_y":307,"ground2_tilt_angle":0,"ground3_tilt_angle":0,"leaning_angle":0}}
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
      "channel_id": 1,
      "camera_name": "DS362",
      "res_height": 1080,
      "res_width": 1920,
      "confidence": 100,
      "confidence2": 0,
      "progress_bar": 0,
      "engine_type": 4,
      "label_name": "person",
      "class_id": 0,
      "obj_type": 0,
      "obj_tracking_id": 293,
      "obj_dwell_time": 301,
      "tof_distance": 1.3609999418258667,
      "tof_height": 1.3055000305175781,
      "max_height_x": 124,
      "max_height_y": 169,
      "tof_height_velocity": -0.0018666585674509406,
      "x": 210,
      "y": 370,
      "w": 666,
      "h": 705,
      "center_direction": "",
      "parent_idx": -1,
      "min_distance": 0,
      "max_distance": 0,
      "min_height": 0,
      "max_height": 0,
      "detection_zone_id": 0,
      "detection_zone_id2": 0,
      "detection_zone_id3": 0,
      "detection_zone_id4": 0,
      "behavior_id": 0
    },
    {
      "id": 1,
      "channel_id": 1,
      "camera_name": "DS362",
      "res_height": 1080,
      "res_width": 1920,
      "confidence": 100,
      "confidence2": 0,
      "progress_bar": 0,
      "engine_type": 4,
      "label_name": "tof_point",
      "class_id": 1000,
      "obj_type": 0,
      "obj_tracking_id": 339,
      "obj_dwell_time": 4,
      "tof_distance": 0,
      "tof_height": 0,
      "max_height_x": 0,
      "max_height_y": 0,
      "tof_height_velocity": 0,
      "x": 1512,
      "y": 1071,
      "w": 60,
      "h": 45,
      "center_direction": "",
      "parent_idx": -1,
      "min_distance": 964,
      "max_distance": 0,
      "min_height": 772,
      "max_height": 0,
      "detection_zone_id": 0,
      "detection_zone_id2": 0,
      "detection_zone_id3": 0,
      "detection_zone_id4": 0,
      "behavior_id": 0
    },
    {
      "id": 2,
      "channel_id": 1,
      "camera_name": "DS362",
      "res_height": 1080,
      "res_width": 1920,
      "confidence": 100,
      "confidence2": 0,
      "progress_bar": 0,
      "engine_type": 4,
      "label_name": "tof_point",
      "class_id": 1000,
      "obj_type": 0,
      "obj_tracking_id": 336,
      "obj_dwell_time": 27,
      "tof_distance": 0,
      "tof_height": 0,
      "max_height_x": 0,
      "max_height_y": 0,
      "tof_height_velocity": 0,
      "x": 1416,
      "y": 432,
      "w": 60,
      "h": 45,
      "center_direction": "",
      "parent_idx": -1,
      "min_distance": 0,
      "max_distance": 5233,
      "min_height": 0,
      "max_height": 115,
      "detection_zone_id": 0,
      "detection_zone_id2": 0,
      "detection_zone_id3": 0,
      "detection_zone_id4": 0,
      "behavior_id": 0
    }
  ],
  "counter_count": [
    0,
    0,
    0,
    0,
    0,
    0,
    0,
    0
  ],
  "counter_reset_value": [
    0,
    0,
    0,
    0,
    0,
    0,
    0,
    0
  ],
  "counter_operand": [
    "NULL",
    "NULL",
    "NULL",
    "NULL",
    "NULL",
    "NULL",
    "NULL",
    "NULL"
  ],
  "counters": [],
  "Count": 3,
  "configdirty": 0,
  "AI_fps": 8,
  "snap_size": 0,
  "snap_response": "Disable",
  "snap_image": "",
  "AIToF": {
    "Time": "1733218695",
    "min_tof_range": "1.369000",
    "global_min_x": "500",
    "global_min_y": "476",
    "max_tof_range": "5.481000",
    "global_max_x": "472",
    "global_max_y": "192",
    "unit": "m",
    "ground1_Ht": "1.77",
    "ground2_Ht": "1.71",
    "ground3_Ht": "1.75",
    "ground1_x": 425,
    "ground1_y": 264,
    "ground2_x": 344,
    "ground2_y": 330,
    "ground3_x": 382,
    "ground3_y": 307,
    "ground2_tilt_angle": 0,
    "ground3_tilt_angle": 0,
    "leaning_angle": 0
  }
}
```
