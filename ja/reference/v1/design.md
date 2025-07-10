---
isTocVisible: true
---
# Design（刺繍柄）


{% api "刺繍柄保存", method="POST", url="/design" %}

刺繍柄を検索して指定フォルダに保存します。 

### Example:

**API Searching folder からファイル"ABC"を検索し、サーバーのAPI Queueフォルダに保存する**

```
https://localhost/b-net/api/v1/design?file_name=ABC
```

**API Searching folder からファイル"ABC"を検索し、サーバーのAPI Queueフォルダのサブフォルダ"temp"に保存する**

```
https://localhost/b-net/api/v1/design?file_name=ABC&folder=temp
```

**API Searching folder からファイル"ABC"を検索し、名前を"DEF"に変えて、サーバーのAPI Queueフォルダに保存する**

```
https://localhost/b-net/api/v1/design?file_name=ABC&output_name=DEF
```

**API Searching folder からファイル"ABC"を検索し、色替え情報を"C01、C02、C03"に書き換えて、サーバーのAPI Queueフォルダに保存する**

```
https://localhost/b-net/api/v1/design?file_name=ABC&colors={"needles":[1,2,3]}
```

### Query Parameters:

| Name        | Type   | Description                                                                                                |
| :---------- | :----- | :--------------------------------------------------------------------------------------------------------- |
| file_name   | String | 検索するファイル名です。                                                                                   |
| folder      | String | 検索後の出力先です。API Queueフォルダの相対パスを指定します。未指定のとき、API Queueフォルダに保存します。 |
| colors      | Array  | 色替え情報です。                                                                                           |
| output_name | String | 出力するファイル名です。                                                                                   |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


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


{% api "柄情報取得", method="GET", url="/design/info" %}

ジョブテーブル（t_jobs）に登録された柄を取得します。刺繍イメージは取得できません。 

### Example:

**ジョブテーブルからファイル"ZZ"の情報を取得する**

```
https://localhost/b-net/api/v1/design/info?file_name=ZZ
```

### Query Parameters:

| Name      | Type    | Description                                                                                                                                                                               |
| :-------- | :------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| file_name | String  | ファイル名です。パターンマッチが使用できます。必須パラメーターです。                                                                                                                      |
| per_page  | Integer | 取得するページのデータ数です。指定した数量分の柄情報を取得します。                                                                                                                        |
| page      | Integer | ページ番号です。  2以上を指定すると、per_pageの分だけ先頭からずらしてデータを取得します。<br>per_page=10&page=1では #01 ～ #10 となります<br>per_page=10&page=2では #11 ～ #20 となります |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


### Response:

```json
[
    {
        "filename": "ZZ",
        "stitches": 1371,
        "width": 1103,
        "height": 216,
        "fdr3_root": {
            "color_list": [
                {
                    "stitch": 1,
                    "function": "C04"
                },
                {
                    "stitch": 103,
                    "function": "C03"
                }
            ]
        }
    }
]
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

### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}


{% api "アップロード", method="POST", url="/design/upload" %}

刺繍柄をアップロードして指定フォルダに保存します。 

### Example:

**ファイル「ABC.DST」をアップロードし、サーバーのAPI Queueフォルダに保存する**

```
https://localhost/b-net/api/v1/design/upload?file_name=ABC.DST
```

**ファイル「ABC.DST」をアップロードし、サーバーのAPI Queueフォルダのサブフォルダ「temp」に保存する**

```
https://localhost/b-net/api/v1/design/upload?file_name=ABC.DST&folder=temp
```

### Query Parameters:

| Name      | Type   | Description                                                                                                        |
| :-------- | :----- | :----------------------------------------------------------------------------------------------------------------- |
| file_name | String | アップロードするファイル名と拡張子です。バルダンフォーマットとタジマフォーマットに対応しています。                 |
| folder    | String | アップロード後の出力先です。API Queueフォルダの相対パスを指定します。未指定のとき、API Queueフォルダに保存します。 |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:

```json
{
  "design_file": "Base64 design binary ..."
}

```

### Response:

```json
{
    "file_name": [
        "ABC"
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

