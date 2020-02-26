# Face-Data-Server Protocol Definition

This repository define Protocol definition for Face-Data-Server(FDS).
If you want to build any program with FDS(e.g. custom front-end, custom server),
follow this protocol to communicate with each other.

All repositories below should follow this Protocol.

  - [Cj-bc/Face-Data-Server](https://github.com/Cj-bc/Face-data-server)
  - [Cj-bc/faclig](https://github.com/Cj-bc/faclig)
  - [Cj-bc/FDS-Front3D](https://github.com/Cj-bc/FDS-Front3D)
  - [Cj-bc/FDS-controller](https://github.com/Cj-bc/FDS-controller)

# About versioning

Using [Semantic versioning v2.0.0](https://semver.org/spec/v2.0.0.html).


# About Language

Currently there's two definition in Japanese and English.
If those are differ, Japanese one should be correct.
(If you find any mistakes in English version, please PR or issue)

---

Below is the definition of FDS Protocol

# overview

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

# description for each section

| section | data format | optional description |
| :-: |:-:|:-:|
| version number | bMMMMmmmm |　`MMM` specify major version number; `mmm` specify minor version number; semantic versioning |
| data | list of data in binary format |  |

## data

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


# note

- Big endian
- As Python\s `float` is double, `64bit(8byte).
- While the same major version, I plan to add data just after the last expression.
