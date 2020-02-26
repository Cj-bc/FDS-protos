# Face-Data-Server プロトコル仕様書

このレポジトリはFace-Data-Server(FDS)の通信用プロトコルを定義しています。
もし、FDSを利用したプログラムを制作する場合、このプロトコルに従ってください。

以下のレポジトリはこのプロトコルに準拠しているはずです。

  - [Cj-bc/Face-Data-Server](https://github.com/Cj-bc/Face-data-server)
  - [Cj-bc/faclig](https://github.com/Cj-bc/faclig)
  - [Cj-bc/FDS-Front3D](https://github.com/Cj-bc/FDS-Front3D)
  - [Cj-bc/FDS-controller](https://github.com/Cj-bc/FDS-controller)


# バージョニングについて

この仕様書は[セマンティックバージョニング 2.0.0](https://semver.org/spec/v2.0.0.html)を採用しています。


# 言語について

現在、英語と日本語の二カ国語の仕様があります。
もしもこれらに矛盾があった場合、日本語の版が優先されます。
(英語版に間違いが見つかった場合、PRもしくはissueで知らせてください。)

---

以下、FDSのプロトコルを制定します

# 全体像

```
_______________________________________________
| version number (1 byte) | data (n byte)     |
-----------------------------------------------
```

データセクション展開後
```
______________________________________________________________________________________________________________________________________________________________________________________________________________________________
| version number (1 byte) | face_x radian (8 byte) | face_y radian (8 byte) | face_z radian (8 byte) | mouth_height_percent (1 byte) | mouth_width_percent (1 byte) | left_eye_percent (1 byte) | right_eye_percent (1 byte) |
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

# 各部分

| section | データ | 補足 |
| :-: |:-:|:-:|
| version number | bMMMMmmmm |　`MMM`はメジャーバージョン番号; `mmm`はマイナーバージョン番号; セマンティックバージョニング |
| data | データのバイナリ表現の列 |  |

## data

具体的な各値を格納している部分。
現在確定している値は以下のとおり。
又、`data`に並ぶ順番も以下の通りとする。

| 表記                 | 長さ   | 値の範囲 | 単位       |説明                    |
| :-:                  |:-:     |  :-:     | :-:        |:-:                     |
| face_x_radian        | 8 byte | -pi ~ pi | ラジアン値 | 顔のX軸に対する回転    |
| face_y_radian        | 8 byte | -pi ~ pi | ラジアン値 | 顔のY軸に対する回転    |
| face_z_radian        | 8 byte | -pi ~ pi | ラジアン値 | 顔のZ軸に対する回転    |
| mouth_height_percent | 1 byte | 0~150    | 割合       | 口の縦向きの開き具合   |
| mouth_width_percent  | 1 byte | 0~150    | 割合       | 口の横向きの開き具合   |
| left_eye_percent     | 1 byte | 0~150    | 割合       | 左目の縦向きの開き具合 |
| right_eye_percent    | 1 byte | 0~150    | 割合       | 右目の縦向きの開き具合 |


# 備考

- ビッグエンディアンです
- Pythonの`float`は倍精度小数点数であるため、64bit(8byte)。元データを生成するのがPythonなのでそちらに合わせてある。
- メジャーバージョンが変わらない間は、後ろにデータを連ねていく方針

