# History（履歴）


{% api "刺繍完了履歴の取得", method="GET", url="/history/finished" %}

刺繍完了履歴を取得します。

### 概要:

このエンドポイントは、刺繍完了履歴のリストを返します。以下のクエリパラメータを使用して結果をフィルタリングできます：
- 特定のミシンに限定
- 特定のオペレーターに限定
- 特定のグループに限定
- 終了時間の設定
- スパン/間隔の設定（デフォルト：60分）

### Example:

**すべての刺繍完了履歴を取得する**

```
https://localhost/b-net/api/v2/history/finished?span=0
```

**ミシンIDがM00から始まるミシンの刺繍完了履歴を取得する**

```
https://localhost/b-net/api/v2/history/finished?machineID=M00_
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                 |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| machineID       | String  | ミシンIDです。パターンマッチが使用できます。                                                                                                                                                |
| operatorID      | String  | オペレーターIDです。パターンマッチが使用できます。                                                                                                                                          |
| groupName       | String  | グループ名です。パターンマッチは**使用できません**。                                                                                                                                        |
| designFilename  | String  | 柄ファイル名です。パターンマッチが使用できます。                                                                                                                                            |
| fieldList       | String  | 返す値を指定します。「fieldList=フィールド名」の形式で使用します（例: "fieldList=machineID"）。カンマ区切りで複数のフィールドを指定することもできます（例: "fieldList=machineID,operatorID,designFilename"）。                             |
| summarize       | String  | 実行を個別に返すか、セットで小計するかを指定します。"true"または"false"（デフォルト: "true"）                                                                                               |
| span            | Number  | 過去何分間のデータを取得するかを指定します。「現在」からの時間です。（デフォルト: 60）                                                                                                      |
| startDateTime   | String  | 生産の開始日時です。指定した日時より後の履歴を抽出します。                                                                                                                                  |
| endDateTime     | String  | 生産の終了日時です。指定した日時より前の履歴を抽出します。未指定の場合、現在時刻より前の履歴を抽出します。                                                                                  |
| pageSize        | Integer | 1ページあたりの結果数です。                                                                                                                                                                 |
| pageOffset      | Integer | ページオフセットです。                                                                                                                                                                      |
| sortOrder       | String  | 結果のソート順です（"asc"または"desc"）。                                                                                                                                                  |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Response:

```json
{
    "finished": [
        {
            "machineID": "M001",
            "operatorID": "THAD",
            "designFilename": "A1234567",
            "startDateTime": "2024-08-26 12:52:01",
            "endDateTime": "2024-08-26 12:55:05",
            "qtyFinished": 1,
            "sewnStitches": 1295,
            "groupIDList": null,
            "groupNameList": null,
            "productionNo": "2"
        },
        {
            "machineID": "M002",
            "operatorID": "Tom",
            "designFilename": "DEMPA",
            "startDateTime": "2025-04-25 19:20:02",
            "endDateTime": "2025-04-25 21:54:50",
            "qtyFinished": 120,
            "sewnStitches": 704418,
            "groupIDList": [
                "G001"
            ],
            "groupNameList": [
                "New group_G001'"
            ],
            "productionNo": null
        }
    ]
}
```

### Fields:

| Name            | Type    | Description              |
| :-------------- | :------ | :----------------------- |
| machineID      | String  | ミシンIDです。           |
| operatorID     | String  | オペレーターIDです。     |
| designFilename  | String  | ファイル名です。         |
| startDateTime | String  | 開始日時です。           |
| endDateTime   | String  | 終了日時です。           |
| qtyFinished   | Integer | 完了した生産枚数です。   |
| sewnStitches  | Integer | 刺繍したステッチ数です。 |
| groupIDList   | Array   | グループIDの配列です。   |
| groupNameList | Array   | グループ名の配列です。   |
| productionNo  | String  | 生産番号です。           |


### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | コンテンツなし。               |
| 400  | 不正なリクエスト。             |
| 401  | 認証エラー。                   |
| 404  | リソースが見つかりません。     |
| 409  | リソースの競合。               |
| 503  | サービス利用不可。             |

{% endapi %}

{% api "刺繍エラー発生履歴の取得", method="GET", url="/history/errors" %}

刺繍エラー発生履歴を取得します。

### 概要:

このエンドポイントは、刺繍エラー発生履歴のリストを返します。以下のクエリパラメータを使用して結果をフィルタリングできます：
- 特定のミシンに限定
- 特定のオペレーターに限定
- 特定のグループに限定
- 終了時間の設定
- スパン/間隔の設定（デフォルト：60分）

### Example:

**すべてのエラー発生履歴を取得する**

```
https://localhost/b-net/api/v2/history/errors?span=0
```

**特定のデザインファイルに関連するエラー発生履歴を取得する**

```
https://localhost/b-net/api/v2/history/errors?designFilename=D013923
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                 |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| machineID       | String  | ミシンIDです。パターンマッチが使用できます。                                                                                                                                                |
| operatorID      | String  | オペレーターIDです。パターンマッチが使用できます。                                                                                                                                          |
| groupName       | String  | グループ名です。パターンマッチは**使用できません**。                                                                                                                                        |
| designFilename  | String  | 柄ファイル名です。パターンマッチが使用できます。                                                                                                                                            |
| fieldList       | String  | 返す値を指定します。「fieldList=フィールド名」の形式で使用します（例: "fieldList=machineID"）。カンマ区切りで複数のフィールドを指定することもできます（例: "fieldList=machineID,operatorID,designFilename"）。                             |
| span            | Number  | 過去何分間のデータを取得するかを指定します。終了日時からの時間です。終了日時が指定されていない場合、「現在」からの時間です。（デフォルト: 60）                                              |
| startDateTime   | String  | 生産の開始日時です。指定した日時より後の履歴を抽出します。                                                                                                                                  |
| endDateTime     | String  | 生産の終了日時です。指定した日時より前の履歴を抽出します。未指定の場合、現在時刻より前の履歴を抽出します。                                                                                  |
| pageSize        | Integer | 1ページあたりの結果数です。                                                                                                                                                                 |
| pageOffset      | Integer | ページオフセットです。                                                                                                                                                                      |
| sortOrder       | String  | 結果のソート順です（"asc"または"desc"）。                                                                                                                                                  |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Response:

```json
{
    "errors": [
        {
            "machineID": "M001",
            "operatorID": "Jason",
            "designFilename": "A1234567",
            "startDateTime": "2025-04-26 15:36:02",
            "endDateTime": "2025-04-26 15:38:35",
            "eventCode": "D16",
            "stitches": 1011,
            "groupIDList": [
                "G001"
            ],
            "groupNameList": [
                "New group_G001'"
            ],
            "productionNo": "HTA2024"
        },
        {
            "machineID": "M002",
            "operatorID": "Tom",
            "designFilename": "DEMPA",
            "startDateTime": "2025-04-26 17:47:48",
            "endDateTime": "2025-04-26 17:50:15",
            "eventCode": "D16",
            "stitches": 1523,
            "groupIDList": [
                "G001"
            ],
            "groupNameList": [
                "New group_G001'"
            ],
            "productionNo": null
        },
    ]
}
```

### Fields:

| Name            | Type   | Description            |
| :-------------- | :----- | :--------------------- |
| machineID      | String | ミシンIDです。         |
| operatorID     | String | オペレーターIDです。   |
| designFilename       | String | ファイル名です。       |
| startDateTime | String | エラー発生日時です。   |
| endDateTime   | String | エラー完了日時です。   |
| eventCode      | String | イベントコードです。   |
| stitches      | Integer | エラー発生針数です。   |
| groupIDList   | Array  | グループIDの配列です。 |
| groupNameList | Array  | グループ名の配列です。 |
| productionNo      | String | 生産番号です。         |


### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | コンテンツなし。               |
| 400  | 不正なリクエスト。             |
| 401  | 認証エラー。                   |
| 404  | リソースが見つかりません。     |
| 409  | リソースの競合。               |
| 503  | サービス利用不可。             |

{% endapi %}

{% api "ジョブ履歴の取得", method="GET", url="/history/jobstats" %}

ジョブ履歴を取得します。

### 概要:

このエンドポイントは、ジョブ履歴のリストを返します。以下のクエリパラメータを使用して結果をフィルタリングできます：
- 特定のミシンに限定
- 特定のオペレーターに限定
- 特定のグループに限定
- 終了時間の設定
- スパン/間隔の設定（デフォルト：60分）

### Example:

**すべてのジョブ履歴を取得する**

```
https://localhost/b-net/api/v2/history/jobstats?span=0
```

**特定の生産番号に関連するジョブ履歴を取得する**

```
https://localhost/b-net/api/v2/history/jobstats?productionNo=D013923
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                 |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| machineID       | String  | ミシンIDです。パターンマッチが使用できます。                                                                                                                                                |
| operatorID      | String  | オペレーターIDです。パターンマッチが使用できます。                                                                                                                                          |
| groupName       | String  | グループ名です。パターンマッチは**使用できません**。                                                                                                                                        |
| designFilename  | String  | 柄ファイル名です。パターンマッチが使用できます。                                                                                                                                            |
| fieldList       | String  | 返す値を指定します。「fieldList=フィールド名」の形式で使用します（例: "fieldList=machineID"）。カンマ区切りで複数のフィールドを指定することもできます（例: "fieldList=machineID,operatorID,designFilename"）。                             |
| productionNo    | String  | 生産番号です。                                                                                                                                                                |
| span            | Number  | 過去何分間のデータを取得するかを指定します。終了日時からの時間です。終了日時が指定されていない場合、「現在」からの時間です。（デフォルト: 60）                                              |
| startDateTime   | String  | 生産の開始日時です。指定した日時より後の履歴を抽出します。                                                                                                                                  |
| endDateTime     | String  | 生産の終了日時です。指定した日時より前の履歴を抽出します。未指定の場合、現在時刻より前の履歴を抽出します。                                                                                  |
| pageSize        | Integer | 1ページあたりの結果数です。                                                                                                                                                                 |
| pageOffset      | Integer | ページオフセットです。                                                                                                                                                                      |
| sortOrder       | String  | 結果のソート順です（"asc"または"desc"）。                                                                                                                                                  |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Response:

```json
{
    "jobstats": [
        {
            "machineID": "M001",
            "designFilename": "A1234567",
            "productionNo": "HTA2024",
            "startDateTime": "2025-04-26 10:43:48",
            "endDateTime": "2025-04-26 12:38:27",
            "qtyStarted": 120,
            "qtyFinished": 120,
            "sewnStitches": 164388,
            "cleanupTime": "01:44:23",
            "setupTime": "00:04:12",
            "sewingTime": "00:01:50",
            "runningTime": "00:16:00",
            "totalErrorTime": "00:00:00",
            "threadBreakTime": "00:00:00",
            "groupIDList": [
                "G001"
            ],
            "groupNameList": [
                "New group_G001'"
            ],
            "operatorIDList": [
                "Jason Statham"
            ]
        },
        {
            "machineID": "M001",
            "designFilename": "A1234567",
            "productionNo": "HTA2024",
            "startDateTime": "2025-04-26 12:38:27",
            "endDateTime": "2025-04-26 14:32:33",
            "qtyStarted": 120,
            "qtyFinished": 120,
            "sewnStitches": 164400,
            "cleanupTime": "01:43:54",
            "setupTime": "00:04:14",
            "sewingTime": "00:01:51",
            "runningTime": "00:16:04",
            "totalErrorTime": "00:00:00",
            "threadBreakTime": "00:00:00",
            "groupIDList": [
                "G001"
            ],
            "groupNameList": [
                "New group_G001'"
            ],
            "operatorIDList": [
                "Jason Statham"
            ]
        }
    ]
}
```

### Fields:

| Name              | Type    | Description                                                          |
| :---------------- | :------ | :------------------------------------------------------------------- |
| machineID        | String  | ミシンIDです。                                                       |
| designFilename   | String  | ファイル名です。                                                     |
| productionNo     | String  | 生産番号です。                                                       |
| startDateTime    | String  | ジョブ開始日時です。                                                 |
| endDateTime      | String  | ジョブ完了日時です。（ジョブが継続している場合には集計日時）           |
| qtyStarted       | Integer | このジョブで開始した生産の総数です。                                 |
| qtyFinished      | Integer | このジョブで完了した生産の総数です。                                 |
| sewnStitches     | Integer | このジョブで実際に刺繍した総針数です。                               |
| cleanupTime      | String  | このジョブの後工程作業（刺繍完了後、運転セット解除まで）の時間です。   |
| setupTime        | String  | このジョブの準備作業（運転セット後、刺繍開始まで）の時間です。         |
| sewingTime       | String  | このジョブの刺繍作業（刺繍開始後、刺繍完了まで）の時間です。           |
| runningTime      | String  | このジョブの刺繍作業時間のうち、ミシンが刺繍した時間です。             |
| totalErrorTime   | String  | このジョブのエラー時間です。                                        |
| threadBreakTime  | String  | このジョブのエラー時間のうち、上糸切れと下糸切れの時間です。           |
| groupIDList      | Array   | グループIDの配列です。                                             |
| groupNameList    | Array   | グループ名の配列です。                                             |
| operatorIDList   | Array   | オペレーターIDの配列です。                                         |

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | コンテンツなし。               |
| 400  | 不正なリクエスト。             |
| 401  | 認証エラー。                   |
| 404  | リソースが見つかりません。     |
| 409  | リソースの競合。               |
| 503  | サービス利用不可。             |

{% endapi %}
