---
isTocVisible: true
---
# Design（刺繍柄）


{% api "アップロード", method="POST", url="/design" %}

刺繍柄をアップロードして指定フォルダに保存します。 

### Example:

**ファイル「ABC」をアップロードし、サーバーのAPI Queueフォルダに保存する**

```
https://localhost/b-net/api/dev/design?file_name=ABC
```

### Query Parameters:

| Name      | Type   | Description                                                                                                |
| :-------- | :----- | :--------------------------------------------------------------------------------------------------------- |
| file_name | String | 出力するファイル名です。                                                                                   |
| folder    | String | 検索後の出力先です。API Queueフォルダの相対パスを指定します。未指定のとき、API Queueフォルダに保存します。 |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:

```json
{
    "fdr3": {
        "product_number": "312-01",
        "item_name": "item#1",
        "product_type": "A",
        "qty": 1,
        "speed_start": 1000,
        "speed_max": 1100,
        "frame_name": "18cm Blue Round",
        "frame_outline_name": "18CM50",
        "backing_type": "2 layers of solvy.",
        "where_to_sew": "Left Pocket",
        "operator": "robert",
        "memo": "Sew, trim & bag",
        "due": {
            "year": 2022,
            "month": 12,
            "day": 1,
            "hour": 22,
            "minute": 18
        },
        "frame_info": {
            "offset_h": 10,
            "offset_v": 50,
            "p1_h": 210,
            "p1_v": 4,
            "p2_h": 2600,
            "p2_v": -1600
        },
        "double_byte_characters": false,
        "local_design_name": "AcmeCorporateLogo",
        "image": "Base64 image binary ..."
    },
    "fdr3_palette": {
      "first_stitch_color": "C15",
      "background_color": "#F0FF00",
      "threads": [
        {
          "needle": 1,
          "color": "C01",
          "speed_max": 600,
          "serial": "1801",
          "name": "White",
          "thread_type": "Madeira Polyneon",
          "rgb": "#FEFEFE"
        },
        {
          "needle": -1,
          "color": "C02",
          "speed_max": 600,
          "serial": "1800",
          "name": "Black",
          "thread_type": "Madeira Polyneon",
          "rgb": "#010101"
        },
        {
          "needle": -1,
          "color": "C03",
          "speed_max": 800,
          "serial": "1755",
          "name": "Red",
          "thread_type": "Madeira Polyneon",
          "rgb": "#800000"
        }
      ]
    },
    "prj_info": {
      "v_scale": 100,
      "h_scale": 200,
      "rot_pattern": 1,
      "angle": 0,
      "origin": 1,
      "socks": 1,
      "applique": 0,
      "a_h_offset": 0,
      "a_v_offset": 0,
      "frame_out": 0,
      "f_h_offset": 0,
      "f_v_offset": 0,
      "cap_frame": 0,
      "frame_type": 0,
      "repeat": 1,
      "matrix": 0,
      "v_repeat": 1,
      "h_repeat": 1,
      "v_space": 0,
      "h_space": 0,
      "start_dir": 0,
      "swing_type": 0,
      "frm_offset_h": 0,
      "frm_offset_v": 0,
      "frm_p1_h": 0,
      "frm_p1_v": 0,
      "frm_p2_h": 0,
      "frm_p2_v": 0
    },
    "needles": [
      5,
      4,
      3
    ],
    "design_file": "Base64 design binary ..."
}

```

### Request Body Parameters:

| Name                   | Type    | Description                                                                                                                      |
| :--------------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------- |
| <b>fdr3</b>            | Object  | FDR3の生産条件生産指示情報を入力します。                                                                                         |
| product_number         | String  | 生産番号です。                                                                                                                   |
| item_name              | String  | 製品名です。                                                                                                                     |
| product_type           | String  | 生産区分です。A、B、C、Zのいずれかを設定します。小文字でも設定可能です。                                                         |
| qty                    | Integer | 枚数です。                                                                                                                       |
| speed_start            | Integer | 開始回転数です。                                                                                                                 |
| speed_max              | Integer | 最高回転数です。                                                                                                                 |
| frame_name             | String  | 枠名です。                                                                                                                       |
| frame_outline_name     | String  | 枠外形名です。                                                                                                                   |
| backing_type           | String  | バッキング名です。                                                                                                               |
| where_to_sew           | String  | 刺繍位置です。                                                                                                                   |
| operator               | String  | 作業者IDです。                                                                                                                   |
| memo                   | String  | メモです。                                                                                                                       |
| due                    | Object  | 納期です。                                                                                                                       |
| frame_info             | Object  | 枠位置情報です。                                                                                                                 |
| double_byte_characters | String  | 地域文字ビットフラグです。trueにすると地域文字を使用します。falseのときは地域文字を使用できません。                              |
| local_design_name      | String  | 地域柄名です。日本語などの2バイトを使用する場合にはdouble_byte_charactersをtrueにしてください。                                  |
| image                  | String  | イメージです。PNG画像かJPG画像のBase64エンコード文字を設定します。QVGAより大きな画像を設定すると、変換に失敗する恐れがあります。 |
| <b>fdr3_palette</b>    | Object  | FDR3の生産条件糸指示情報を入力します。                                                                                           |
| first_stitch_color     | String  | 0stファンクションです。                                                                                                          |
| background_color       | String  | 背景色です。RGBに変換できない文字列はエラーになります。                                                                          |
| threads                | Object  | 糸指示詳細情報です。糸指示詳細情報の配列です。                                                                                   |
| needle                 | Integer | 針棒番号です。                                                                                                                   |
| color                  | String  | カラーファンクション番号です。                                                                                                   |
| speed_max              | Integer | 最高回転数です。                                                                                                                 |
| serial                 | String  | シリアル番号です。必須パラメーターです。                                                                                         |
| name                   | String  | 糸色名です。必須パラメーターです。                                                                                               |
| thread_type            | String  | 糸タイプです。必須パラメーターです。                                                                                             |
| rgb                    | String  | 糸色です。RGBに変換できない文字列はエラーになります。必須パラメーターです。                                                      |
| <b>prj_info</b>        | Object  | PRJ情報を入力します。                                                                                                            |
| v_scale                | Integer | Ｖ倍率です。                                                                                                                     |
| h_scale                | Integer | Ｈ倍率です。                                                                                                                     |
| rot_pattern            | Integer | 回転パターンです。                                                                                                               |
| angle                  | Integer | 回転角度です。                                                                                                                   |
| origin                 | Integer | 自動原点復帰です。                                                                                                               |
| socks                  | Integer | 靴下縫いです。                                                                                                                   |
| applique               | Integer | アップリケ移動です。                                                                                                             |
| a_h_offset             | Integer | アップリケＨ移動量です。                                                                                                         |
| a_v_offset             | Integer | アップリケＶ移動量です。                                                                                                         |
| frame_out              | Integer | 自動枠交換移動です。                                                                                                             |
| f_h_offset             | Integer | 枠交換Ｈ移動量です。                                                                                                             |
| f_v_offset             | Integer | 枠交換Ｖ移動量です。                                                                                                             |
| cap_frame              | Integer | 帽子枠です。                                                                                                                     |
| frame_type             | Integer | 枠種類です。                                                                                                                     |
| repeat                 | Integer | 繰返し数です。                                                                                                                   |
| matrix                 | Integer | マトリックスです。                                                                                                               |
| v_repeat               | Integer | Ｖ回数です。                                                                                                                     |
| h_repeat               | Integer | Ｈ回数です。                                                                                                                     |
| v_space                | Integer | Ｖ隙間です。                                                                                                                     |
| h_space                | Integer | Ｈ隙間です。                                                                                                                     |
| start_dir              | Integer | 開始方向です。                                                                                                                   |
| swing_type             | Integer | 振り幅強調のタイプです。                                                                                                         |
| frm_offset_h           | Integer | 枠位置Ｈ移動量です。                                                                                                             |
| frm_offset_v           | Integer | 枠位置V移動量です。                                                                                                              |
| frm_p1_h               | Integer | 枠位置P1のH位置です。                                                                                                            |
| frm_p1_v               | Integer | 枠位置P1のV位置です。                                                                                                            |
| frm_p2_h               | Integer | 枠位置P2のH位置です。                                                                                                            |
| frm_p2_v               | Integer | 枠位置P2のV位置です。                                                                                                            |
| <b>needles</b>         | Array   | 色替え先針棒番号の配列です。                                                                                                     |
| <b>design_file</b>     | String  | アップロードする刺繍柄です。Base64エンコード文字を設定します。                                                                 |


### Response:

```json
{
    "file_name": [
        "123456789"
    ]
}
```

### Fields:

| Name      | Type  | Description              |
| :-------- | :---- | :----------------------- |
| file_name | Array | 保存したファイル名です。 |


### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}
