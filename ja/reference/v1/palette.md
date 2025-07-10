# Palette（糸色パレット）


{% api "糸色パレット登録", method="POST", url="/palette/threads" %}

糸色パレットを登録します。

### Example:

**糸色パレットを登録する**

```
https://localhost/b-net/api/v1/palette/threads
```

### Query Parameters:

| Name | Type | Description              |
| :--- | :--- | :----------------------- |
| ---  | ---  | パラメータはありません。 |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:

```json
{
  "items": [
    {
      "serial": "Color01",
      "threadtype": "type",
      "name": "White",
      "rgb": "#FFFFFF"
    },
    {
      "serial": "Color02",
      "threadtype": "type",
      "name": "Black",
      "rgb": "#000000"
    }
  ]
}
```

### Request Body Parameters:

| Name       | Type   | Description                                           |
| :--------- | :----- | :---------------------------------------------------- |
| serial     | String | シリアル番号です。                                    |
| threadtype | String | 糸タイプです。                                        |
| name       | String | 糸色名です。                                          |
| rgb        | String | 糸色です。RGBに変換できない文字列はエラーになります。 |

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

{% api "糸色パレット取得", method="GET", url="/palette/threads" %}

糸色パレットを取得します。 

### Example:

**すべての糸色を取得する（最大500）**

```
https://localhost/b-net/api/v1/palette/threads
```

**糸タイプがAngelking #6 Halfの糸色を取得する**

```
https://localhost/b-net/api/v1/palette/threads?filter:threadtype=Angelking%20%236%20Half
```

**糸色が#FFFFFFの糸色を取得する**

```
https://localhost/b-net/api/v1/palette/threads?filter:rgb=%23FFFFFF
```

### Query Parameters:

| Name     | Type    | Description                                                                                                                                                                               |
| :------- | :------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| per_page | Integer | 取得するページのデータ数です。指定した数量分の情報を取得します。                                                                                                                          |
| page     | Integer | ページ番号です。  2以上を指定すると、per_pageの分だけ先頭からずらしてデータを取得します。<br>per_page=10&page=1では #01 ～ #10 となります<br>per_page=10&page=2では #11 ～ #20 となります |
| filter   | String  | 取得するデータのフィルターです。                                                                                                                                                          |

### Filter:

| Name          | Type    | Description                                                    |
| :------------ | :------ | :------------------------------------------------------------- |
| serial        | String  | 糸色のシリアル番号です。パターンマッチが使用できます。         |
| color         | String  | 糸色名です。パターンマッチが使用できます。                     |
| rgb           | String  | 糸色（RGB文字列）です。パターンマッチが使用できます。          |
| threadtype    | String  | 糸タイプです。パターンマッチが使用できます。                   |
| maxspeed      | Integer | 最高回転数です。                                               |
| maxspeed_more | Integer | 最高回転数です。指定を超える最高回転数の糸情報を抽出します。   |
| maxspeed_less | Integer | 最高回転数です。指定に満たない最高回転数の糸情報を抽出します。 |


### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


### Response:

```json
[
    {
        "palette_id": 117540,
        "serial": "700",
        "color": "Mars Red",
        "rgb": "#E41C17",
        "threadtype": "NULL",
        "metadata": {
            "memo": ""
        }
    },
    {
        "palette_id": 117542,
        "serial": "702",
        "color": "Fire Engine Red",
        "rgb": "#E21916",
        "threadtype": "NULL",
        "metadata": null
    },
    {
        "palette_id": 117543,
        "serial": "703",
        "color": "Ruby Red",
        "rgb": "#E62423",
        "threadtype": "NULL",
        "metadata": null
    }
]
```

### Fields:

| Name       | Type    | Description        |
| :--------- | :------ | :----------------- |
| palette_id | Integer | パレットIDです。   |
| serial     | String  | シリアル番号です。 |
| color      | String  | 糸色名です。       |
| rgb        | String  | 糸色のRGBです。    |
| threadtype | String  | 糸タイプです。     |
| metadata   | JSON    | メタデータです。   |


### Errors:

| Code | Description                  |
| :--- | :--------------------------- |
| 404  | リソースが見つかりません。   |
| 500  | 内部でエラーが発生しました。 |

{% endapi %}

{% api "糸色パレット削除", method="DELETE", url="/palette/threads" %}

糸色パレットを削除します。 

### Example:

**パレットID"12345"の糸色を削除する**

```
https://localhost/b-net/api/v1/palette/threads?palette_id=12345
```

### Query Parameters:

| Name       | Type    | Description                            |
| :--------- | :------ | :------------------------------------- |
| palette_id | Integer | パレットIDです。必須パラメーターです。 |

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
