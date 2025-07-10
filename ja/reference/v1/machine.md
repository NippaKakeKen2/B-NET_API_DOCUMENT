---
isTocVisible: true
---
# Machine (ミシン)

## ステータス
{% api "ステータス取得", method="GET", url="/machine/status" %}

ミシンのステータスを取得します

### Example:

**すべてのミシンのステータスを取得する**
```
https://localhost/b-net/api/v1/machine/status
```

**IDがM001のミシンのステータスを取得する**
```
https://localhost/b-net/api/v1/machine/status?filter:machine_id=M001
```

### Query Parameters:

| Name     | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                    |
| :------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| per_page | Integer | 取得するページのデータ数です。指定した数量分のミシン情報を取得します。                                                                                                                                                                                                                                                                                                                                         |
| page     | Integer | ページ番号です。  2以上を指定すると、per_pageの分だけ先頭からずらしてデータを取得します。<br>per_page=10&page=1では #01 ～ #10 となります<br>per_page=10&page=2では #11 ～ #20 となります                                                                                                                                                                                                                      |
| fields   | String  | 取得するデータのフィールド名です。<br>指定しない場合、すべての情報を取得します。<br>指定する場合のフィールド名は、戻り値のキー名を参照してください。                                                                                                                                                                                                                                                           |
| order    | String  | 取得するデータの並びです。<br>order=needle ASC,machineid DESC<br>のように指定すると針棒数の昇順かつミシンIDの降順で取得します。<br>ASC（昇順）やDESC（降順）を省略した場合、昇順で取得します。<br>指定する場合のフィールド名は、戻り値のキー名を参照してください。<br>ただし、groupid,groupname は使用できません。<br>このパラメーターを省略した場合、machineidの昇順で取得します。 |
| filter   | String  | 取得するデータのフィルターです。<br>filter:machine_id=M%&#124;needle=9<br>のように指定すると、IDがMから始まる9本針のミシン情報を取得します。<br>フィルターに使用できる情報は次表を参照してください。                                                                                                                                                                                                           |


### Filter:

| Name                 | Type    | Description                                                                                |
| :------------------- | :------ | :----------------------------------------------------------------------------------------- |
| machine_id           | String  | ミシンIDです。パターンマッチが使用できます。                                               |
| jcode                | String  | イベントです。指定したイベントと一致するミシンを抽出します。パターンマッチが使用できます。 |
| jcode_exc            | String  | イベントです。指定したイベントを一致するミシンを除外します。パターンマッチが使用できます。 |
| model                | String  | モデル名です。パターンマッチが使用できます。                                               |
| operator_name        | String  | オペレーター名です。パターンマッチは**使用できません**。                                   |
| operator_id          | String  | オペレーターIDです。パターンマッチが使用できます。                                         |
| design_name          | String  | 柄名です。パターンマッチが使用できます。                                                   |
| group_name           | String  | グループ名です。パターンマッチは**使用できません**。                                       |
| group_id             | String  | グループIDです。パターンマッチが使用できます。                                             |
| head                 | Integer | 頭部数です。                                                                               |
| needle               | Integer | 針棒数です。                                                                               |
| needle_more          | Integer | 針棒数です。                                                                               |
| needle_less          | Integer | 針棒数です。                                                                               |
| remaining_time       | String  | 残り作業時間です。「時:分:秒」形式で指定します。指定に一致するミシンを抽出します。         |
| remaining_time _more | String  | 残り作業時間です。「時:分:秒」形式で指定します。指定を超えるミシンを抽出します。           |
| remaining_time _less | String  | 残り作業時間です。「時:分:秒」形式で指定します。指定に満たないミシンを抽出します。         |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Returns:

```json
[
  {
  "machineid": "M001",
  "model": "BEKS",
  "operatorid": "-",
  "operatorname": null,
  "head": null,
  "effectivehead": null,
  "errorheadtext": null,
  "needle": 9,
  "designname": "-",
  "designfullname": "-",
  "totalstitchcount": 0,
  "sewingspeed": 0,
  "machinesewingspeed": 1300,
  "jcode": "Disconnect",
  "jcodealternativetext": "Disconnect",
  "currentstitchcount": 0,
  "remainingtime": "00:00:00",
  "groupid": null,
  "groupname": null
  },
  {
    "machineid": "M002",
    ...
  }
]
```

### Fields:

| Name                   | Type    | Description              |
| :--------------------- | :------ | :----------------------- |
| machineid             | String  | ミシンIDです。           |
| model                  | String  | モデル名です。           |
| operatorid            | String  | オペレーターIDです。     |
| operatorname          | String  | オペレーター名です。     |
| head                   | Integer | 頭部数です。             |
| effectivehead         | Integer | 有効頭部数です。         |
| errorheadtext        | String  | エラー頭部位置です。     |
| needle                 | Integer | 針棒数です。             |
| designname            | String  | 柄名です。               |
| designfullname       | String  | 柄のフルパスです。       |
| totalstitchcount     | String  | 柄の総針数です。           |
| sewingspeed           | Integer | 刺繍速度です。           |
| machinesewingspeed   | Integer | 機械設定の刺繍速度です。 |
| jcode                  | String  | 状態コードです。         |
| jcodealternativetext | String  | 状態コードの説明です。   |
| currentstitchcount   | Integer | 現在の針数です           |
| remainingtime         | String  | 残り時間です             |
| groupid               | String  | グループIDです           |
| groupname             | String  | グループ名です           |

### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}


## スケジュール

{% api "スケジュール登録", method="POST", url="/machine/schedule" %}

### Example:

**ファイルABCの名前をDEFに変えてミシンM001に送信する**

```
https://localhost/b-net/api/v1/machine/schedule?machine_id=M001&file_name=ABC&output_name=DEF
```

**ファイルABCの色替え情報をC01、C02、C03に書き換えて、ミシンM001に送信する**

```
https://localhost/b-net/api/v1/machine/schedule?machine_id=M001&file_name=ABC&colors={"needles":[1,2,3]}
```

### Query Parameters:


| Name       | Type   | Description                                    |
| :--------- | :----- | :--------------------------------------------- |
| machine_id | String | ミシンIDです。パターンマッチは使用できません。 |
| file_name  | String | ファイル名です。                               |
| colors     | JSON   | 色替え情報です。                               |
| output_name | String | 出力するファイル名です 。                    |
| job | String | ジョブテーブル（t_jobs）への書き込み動作です。<br>none：何もしません<br>add：ジョブテーブルに追加します  |


### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:

### Response:

```json
{
    "file_name": "Number"
}
```

### Fields:

| Name      | Type   | Description                      |
| :-------- | :----- | :------------------------------- |
| file_name | String | ミシンに送信したファイル名です。 |

### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}

{% api "スケジュール取得", method="GET", url="/machine/schedule" %}

### Example:

**ミシンM001のスケジュールを取得する**

```
https://localhost/b-net/api/v1/machine/schedule?machine_id=M001
```

**すべてのミシンのスケジュールを取得する**

```
https://localhost/b-net/api/v1/machine/schedule
```

### Query Parameters:

| Name       | Type    | Description                                                                                                                                                                               |
| :--------- | :------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| machine_id | String  | ミシンIDです。パターンマッチは使用できません。                                                                                                                                            |
| per_page   | Integer | 取得するページのデータ数です。指定した数量分のミシン情報を取得します。                                                                                                                    |
| page       | Integer | ページ番号です。  2以上を指定すると、per_pageの分だけ先頭からずらしてデータを取得します。<br>per_page=10&page=1では #01 ～ #10 となります<br>per_page=10&page=2では #11 ～ #20 となります |
### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


### Response:

```json
[
    {
        "machineid": "KT001",
        "schedules": [
            "ABC(1)"
        ]
    }
]
```

### Fields:

| Name      | Type   | Description                |
| :-------- | :----- | :------------------------- |
| machineid | String | ミシンIDです。             |
| schedules | Array  | ミシンのスケジュールです。 |

### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}

{% api "スケジュール柄取得", method="GET", url="/machine/schedule/design" %}

### Example:

**ミシン"M001"のスケジュールの1番目の情報を取得する**

```
https://localhost/b-net/api/v1/machine/schedule/design/?machine_id=M001&schedule_number=1
```

### Query Parameters:

| Name            | Type    | Description                                                            |
| :-------------- | :------ | :--------------------------------------------------------------------- |
| machine_id      | String  | ミシンIDです。パターンマッチが使用できます。必須パラメーターです。     |
| schedule_number | Integer | スケジュールの番号です。番号は１から開始します。必須パラメーターです。 |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


### Response:

```json
{
    "file_name": "ABC",
    "stitches": 5059,
    "width": 1594,
    "height": 459,
    "fdr3_root": {
        "color_list": [
            {
                "stitch": 1,
                "function": "C04"
            },
            {
                "stitch": 2,
                "function": "C03"
            }
        ],
        "sewn_image": "Base64 image ..."
    }
}
```

### Fields:

| Name                 | Type    | Description                                |
| :------------------- | :------ | :----------------------------------------- |
| file_name            | String  | ファイル名です。                           |
| stitches             | String  | 針数です。                                 |
| width                | String  | 横幅です。                                 |
| height               | String  | 縦幅です。                                 |
| fdr3_root            | Integer | FDR3およびその他の情報です。               |
| fdr3_root/color_list | Integer | カラーリスト（ファンクションリスト）です。 |
| fdr3_root/sewn_image | String  | 刺繍イメージ（base64）です。               |

### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}


## ジョブ

{% api "ジョブ登録", method="POST", url="/machine/job" %}

ミシンに割り当てられた柄（もしくは割り当て予定の柄）をジョブテーブル（t_jobs）に登録します。FDR3 以外の柄を登録することも可能です。 

### Example:


**ミシン"M001"のファイル"FLOWER"を検索し、ジョブテーブルに登録する**

```
https://localhost/b-net/api/v1/machine/job?machine_id=M001&file_name=FLOWER
```

### Query Parameters:

| Name       | Type   | Description                                    |
| :--------- | :----- | :--------------------------------------------- |
| machine_id | String | ミシンIDです。パターンマッチは使用できません。 |
| file_name  | String | ファイル名です。                               |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


### Response:

```json
{
  "file_name": "Yotto",
  "stitches": 3252,
  "width": 729,
  "height": 558,
  "fdr3_root": {
      "color_list": [
          {
              "stitch": 1,
              "function": "C01"
          },
          {
              "stitch": 818,
              "function": "C02"
          },
          {
              "stitch": 1022,
              "function": "C03"
          },
          {
              "stitch": 1435,
              "function": "C04"
          },
          {
              "stitch": 2032,
              "function": "C05"
          },
          {
              "stitch": 2636,
              "function": "C06"
          },
          {
              "stitch": 2788,
              "function": "C07"
          },
          {
              "stitch": 3252,
              "function": "C01"
          }
      ],
      "sewn_image": "Base64 image ...",
      "fdr3": {
          "speed_start": 700,
          "speed_max": 900,
          "area_design_name": "area_design_name",
          "item_name": "2",
          "frame_name": "",
          "backing": "",
          "position": "",
          "memo": "memo",
          "frame_outline_name": "",
          "operator": "UBE",
          "image": "Base64 image ..."
      },
      "fdr3_palette": {
          "version": 1,
          "start_function": "C01",
          "threads": [
              {
                  "function": "C01",
                  "speed": -1,
                  "thread_no": "0001",
                  "needle": -1,
                  "thread_type": "",
                  "thread_name": "",
                  "thread_color": "#936B4A"
              }
          ]
      }
  },
  "production_no": "2",
  "qty": 1,
  "due": "2016-09-14 15:59:00",
  "division": "A"
}
```

### Fields:

| Name                 | Type    | Description                                |
| :------------------- | :------ | :----------------------------------------- |
| file_name            | String  | ファイル名です。                           |
| stitches             | String  | 針数です。                                 |
| width                | String  | 横幅です。                                 |
| height               | String  | 縦幅です。                                 |
| fdr3_root            | Integer | FDR3およびその他の情報です。               |
| fdr3_root/color_list | Integer | カラーリスト（ファンクションリスト）です。 |
| fdr3_root/sewn_image | String  | 刺繍イメージ（base64）です。               |

### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}

## 糸色

{% api "糸色登録", method="POST", url="/machine/threads" %}
### Example:

**ミシン"M001"の糸色情報を登録する**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001
```

### Query Parameters:

| Name       | Type   | Description                                    |
| :--------- | :----- | :--------------------------------------------- |
| machine_id | String | ミシンIDです。パターンマッチは使用できません。 |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:

```json
{
  "cones": [
    {
      "serial": "100",
      "needle": 1,
      "name": "Black",
      "rgb": "#000000",
      "maxspeed": 900,
      "memo": "ABCDEFG",
      "status": 0
    },
    {
      "serial": "102",
      "needle": 2,
      "threadtype": "Madeira Polyneon #40",
      "name": "White",
      "rgb": "#FFFFFF",
      "maxspeed": 1000,
      "status": 0
    },
    {
      "needle": 3,
      "status": -1,
      "memo": "Broken"
    },
    {
      "serial": "102",
      "needle": 4,
      "threadtype": "Madeira Polyneon #40",
      "name": "White",
      "rgb": "#FFFFFF",
      "status": -2
    }
  ]
}
```

### Request Body Parameters:

| Name       | Type    | Description                                           |
| :--------- | :------ | :---------------------------------------------------- |
| needle     | Integer | 針棒番号です。必須パラメーターです。                  |
| serial     | String  | シリアル番号です。                                    |
| threadtype | String  | 糸タイプです。                                        |
| name       | String  | 糸色名です。                                          |
| rgb        | String  | 糸色です。RGBに変換できない文字列はエラーになります。 |
| maxspeed   | Integer | 最高回転数です。                                      |
| memo       | String  | メモです。                                            |

### Response:

```json
{
    "result": "SUCCESS"
}
```

### Fields:

| Name   | Type   | Description    |
| :----- | :----- | :------------- |
| result | String | 実行結果です。 |

### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}

{% api "糸色取得", method="GET", url="/machine/threads" %}

### Example:

**ミシン"M001"の糸色情報を取得する**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001
```

**ミシン"M001"の針棒番号が1より大きく５未満の糸色情報を取得する**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001&filter:needle_number_more=1|needle_number_less=5
```

### Query Parameters:

| Name       | Type   | Description                                    |
| :--------- | :----- | :--------------------------------------------- |
| machine_id | String | ミシンIDです。パターンマッチは使用できません。 |
| filter     | String | 取得するデータのフィルターです。               |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


### Response:

```json
{
    "machineid": "KT001",
    "cones": [
        {
            "needlenumber": 1,
            "serial": "100",
            "color": "Black",
            "threadtype": "",
            "rgb": "#000000",
            "status": 0,
            "metadata": {
                "maxspeed": 900,
                "memo": "ABCDEFG"
            }
        },
        {
            "needlenumber": 2,
            "serial": "102",
            "color": "White",
            "threadtype": "Madeira Polyneon #40",
            "rgb": "#FFFFFF",
            "status": 0,
            "metadata": {
                "maxspeed": 1000
            }
        },
        {
            "needlenumber": 3,
            "serial": "",
            "color": "",
            "threadtype": "",
            "rgb": "",
            "status": -1,
            "metadata": {
                "memo": "Broken"
            }
        },
        {
            "needlenumber": 4,
            "serial": "102",
            "color": "White",
            "threadtype": "Madeira Polyneon #40",
            "rgb": "#FFFFFF",
            "status": -2,
            "metadata": {}
        }
    ]
}
```

### Fields:

| Name         | Type    | Description        |
| :----------- | :------ | :----------------- |
| needlenumber | Integer | 針棒番号です。     |
| serial       | String  | シリアル番号です。 |
| threadtype   | String  | 糸タイプです。     |
| color        | String  | 糸色名です。       |
| rgb          | String  | 糸色のRGBです。    |
| status       | Integer | 糸立ての状態です。 |
| metadata     | JSON    | メタデータです。   |

### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}

{% api "糸色削除", method="DELETE", url="/machine/threads" %}

### Example:

**ミシン"M001"の糸色情報を削除する**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001
```

**ミシン"M001"の針棒2の糸色情報を取得する**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001&needle_number=2
```


### Query Parameters:

| Name          | Type    | Description                                                          |
| :------------ | :------ | :------------------------------------------------------------------- |
| machine_id    | String  | ミシンIDです。パターンマッチは使用できません。必須パラメーターです。 |
| needle_number | Integer | 針棒番号です。指定がない場合、すべての針棒を削除します。             |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


### Response:

```json
{
    "result": "SUCCESS"
}
```

### Fields:

| Name   | Type   | Description    |
| :----- | :----- | :------------- |
| result | String | 実行結果です。 |

### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}

