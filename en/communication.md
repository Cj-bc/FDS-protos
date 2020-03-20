# Face-Data-Server communication protocol definition

This document define communication protocol and related settings (e.g. port number) for Face-Data-Server

## communication method

Use UDP, multicast.

## Used port number/ multicast group address

|||
|:-:|:-:|
| used port number | 5032 |
| used multicast group address | 226.70.68.83 |

## Application layer protocol

For application layer, use the protocol below:

### overview

```
_______________________________________________
| version number (1 byte) | data (n byte)     |
-----------------------------------------------
```

Expanding `data`
```
______________________________________________________________________________________________________________________________________________________________________________________________________________________________
| version number (1 byte) | face_x radian (8 byte) | face_y radian (8 byte) | face_z radian (8 byte) | mouth_height_percent (1 byte) | mouth_width_percent (1 byte) | left_eye_percent (1 byte) | right_eye_percent (1 byte) |
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

### description for each section

| section | data format | optional description |
| :-: |:-:|:-:|
| version number | bMMMMmmmm |　`MMM` specify major version number; `mmm` specify minor version number; semantic versioning |
| data | list of data in binary format |  |

#### data

Section that holding each value.
Here's table for defined values below.
Those are on the same order.

| expression           | length | range of value | Unit       |description       |
| :-:                  |:-:     |  :-:           | :-:        |:-:                     |
| face_x_radian        | 8 byte | -pi ~ pi       | radian     | Face rotation against X axis |
| face_y_radian        | 8 byte | -pi ~ pi       | radian     | Face rotation against Y axis |
| face_z_radian        | 8 byte | -pi ~ pi       | radian     | Face rotation against Z axis |
| mouth_height_percent | 1 byte | 0~150          | percentage | Mouth height percentage   |
| mouth_width_percent  | 1 byte | 0~150          | percentage | Mouth width percentage   |
| left_eye_percent     | 1 byte | 0~150          | percentage | Left eye height percentage |
| right_eye_percent    | 1 byte | 0~150          | percentage | Right eye height percentage |


### note

- Big endian
- As Python\s `float` is double, `64bit(8byte).
- While the same major version, I plan to add data just after the last expression.
