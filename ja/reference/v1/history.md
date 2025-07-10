# History（履歴）


{% api "刺繍完了履歴の取得", method="GET", url="/history?type=finished" %}

刺繍完了履歴を取得します。

### Example:

**すべての刺繍完了履歴を取得する（最大500）**

```
https://localhost/b-net/api/v1/history?type=finished
```

**ミシンIDがM00から始まるミシンの刺繍完了履歴を取得する**

```
https://localhost/b-net/api/v1/history?type=finished&machine_id=M00_
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                 |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type            | String  | クエリタイプです。finished を指定します。                                                                                                                                                   |
| per_page        | Integer | 取得するページのデータ数です。指定した数量分の情報を取得します。                                                                                                                            |
| page            | Integer | ページ番号です。  2以上を指定すると、per_pageの分だけ先頭からずらしてデータを取得します。<br>per_page=10&page=1では #01 ～ #10 となります<br>per_page=10&page=2では #11 ～ #20 となります。 |
| machine_id      | String  | ミシンIDです。パターンマッチが使用できます。                                                                                                                                                |
| operator_id     | String  | オペレーターIDです。パターンマッチが使用できます。                                                                                                                                          |
| group_id        | String  | グループIDです。パターンマッチは**使用できません**。                                                                                                                                              |
| group_name      | String  | グループ名です。パターンマッチは**使用できません**。                                                                                                                                        |
| file_name       | String  | 柄名です。パターンマッチが使用できます。                                                                                                                                                    |
| production_no   | String  | 生産番号です。パターンマッチが使用できます。                                                                                                                                                |
| start_date_time | String  | 生産の開始日時です。指定した日時より後の履歴を抽出します。                                                                                                                                  |
| end_date_time   | String  | 生産の終了日時です。指定した日時より前の履歴を抽出します。未指定の場合、現在時刻より前の履歴を抽出します。                                                                                  |


### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:

### Request Body Parameters:

### Response:

```json
{
    "finished": [
        {
            "machine_id": "M001",
            "operator_id": "-",
            "file_name": "DEMPA",
            "start_date_time": "2021-09-27 12:35:47",
            "end_date_time": "2021-09-27 12:52:52",
            "qty_finished": 12,
            "sewn_stitches": 70894,
            "group_id_list": null,
            "group_name_list": null,
            "product_no": "2"
        },
        {
            "machine_id": "M002",
            "operator_id": "UBE",
            "file_name": "DEMPA2",
            "start_date_time": "2021-10-29 17:16:56",
            "end_date_time": "2021-10-30 09:50:38",
            "qty_finished": 72,
            "sewn_stitches": 2287640,
            "group_id_list": [
                "G019"
            ],
            "group_name_list": [
                "TEST2"
            ],
            "product_no": null
        }
    ]
}
```

### Fields:

| Name            | Type    | Description              |
| :-------------- | :------ | :----------------------- |
| machine_id      | String  | ミシンIDです。           |
| operator_id     | String  | オペレーターIDです。     |
| file_name       | String  | ファイル名です。         |
| start_date_time | String  | 開始日時です。           |
| end_date_time   | String  | 終了日時です。           |
| qty_finished    | Integer | 完了した生産枚数です。   |
| sewn_stitches   | Integer | 刺繍したステッチ数です。 |
| group_id_list   | Array   | グループIDの配列です。   |
| group_name_list | Array   | グループ名の配列です。   |
| product_no      | String  | 生産番号です。           |


### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 400  | 不正なクエリが指定されました。 |
| 404  | リソースが見つかりません。     |
| 500  | 内部でエラーが発生しました。   |

{% endapi %}

{% api "刺繍エラー発生履歴の取得", method="GET", url="/history?type=errors" %}

刺繍エラー発生履歴を取得します。

### Example:

**すべてのエラー発生履歴を取得する（最大500）**

```
https://localhost/b-net/api/v1/history?type=errors
```

**イベントコードD16のエラー発生履歴を取得する**

```
https://localhost/b-net/api/v1/history?type=errors&event_code=D16
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                 |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type            | String  | クエリタイプです。errors を指定します。                                                                                                                                                   |
| per_page        | Integer | 取得するページのデータ数です。指定した数量分の情報を取得します。                                                                                                                            |
| page            | Integer | ページ番号です。  2以上を指定すると、per_pageの分だけ先頭からずらしてデータを取得します。<br>per_page=10&page=1では #01 ～ #10 となります<br>per_page=10&page=2では #11 ～ #20 となります。 |
| machine_id      | String  | ミシンIDです。パターンマッチが使用できます。                                                                                                                                                |
| operator_id     | String  | オペレーターIDです。パターンマッチが使用できます。                                                                                                                                          |
| group_id        | String  | グループIDです。パターンマッチは**使用できません**。                                                                                                                                              |
| group_name      | String  | グループ名です。パターンマッチは**使用できません**。                                                                                                                                        |
| file_name       | String  | 柄名です。パターンマッチが使用できます。                                                                                                                                                    |
| production_no   | String  | 生産番号です。パターンマッチが使用できます。                                                                                                                                                |
| start_date_time | String  | 生産の開始日時です。指定した日時より後の履歴を抽出します。                                                                                                                                  |
| end_date_time   | String  | 生産の終了日時です。指定した日時より前の履歴を抽出します。未指定の場合、現在時刻より前の履歴を抽出します。                                                                                  |
| event_code      | String  | イベントコードです。パターンマッチが使用できます。                                                                                                                                          |


### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


### Response:

```json
{
    "errors": [
        {
            "machine_id": "M003",
            "operator_id": "Johnny Depp",
            "file_name": "Trump",
            "start_date_time": "2021-10-30 09:20:25",
            "end_date_time": "2021-10-30 09:22:30",
            "event_code": "D16",
            "group_id_list": null,
            "group_name_list": null,
            "product_no": null
        }
    ]
}
```

### Fields:

| Name            | Type   | Description            |
| :-------------- | :----- | :--------------------- |
| machine_id      | String | ミシンIDです。         |
| operator_id     | String | オペレーターIDです。   |
| file_name       | String | ファイル名です。       |
| start_date_time | String | エラー発生日時です。   |
| end_date_time   | String | エラー完了日時です。   |
| event_code      | String | イベントコードです。   |
| group_id_list   | Array  | グループIDの配列です。 |
| group_name_list | Array  | グループ名の配列です。 |
| product_no      | String | 生産番号です。         |


### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 400  | 不正なクエリが指定されました。 |
| 404  | リソースが見つかりません。     |
| 500  | 内部でエラーが発生しました。   |

{% endapi %}

{% api "ジョブ履歴", method="GET", url="/history?type=jobstats" %}

ジョブ履歴を取得します。 

### Example:

**すべてのジョブ履歴を取得する（最大500）**

```
https://localhost/b-net/api/v1/history?type=jobstats
```

**オペレータID"UBE"のジョブ履歴を取得する**

```
https://localhost/b-net/api/v1/history?type=jobstats&operator_id="UBE"
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                 |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type            | String  | クエリタイプです。jobstats を指定します。                                                                                                                                                   |
| per_page        | Integer | 取得するページのデータ数です。指定した数量分の情報を取得します。                                                                                                                            |
| page            | Integer | ページ番号です。  2以上を指定すると、per_pageの分だけ先頭からずらしてデータを取得します。<br>per_page=10&page=1では #01 ～ #10 となります<br>per_page=10&page=2では #11 ～ #20 となります。 |
| machine_id      | String  | ミシンIDです。パターンマッチが使用できます。                                                                                                                                                |
| operator_id     | String  | オペレーターIDです。パターンマッチは**使用できません**。                                                                                                                                          |
| group_id        | String  | グループIDです。パターンマッチは**使用できません**。                                                                                                                                              |
| group_name      | String  | グループ名です。パターンマッチは**使用できません**。                                                                                                                                        |
| file_name       | String  | 柄名です。パターンマッチが使用できます。                                                                                                                                                    |
| production_no   | String  | 生産番号です。パターンマッチが使用できます。                                                                                                                                                |
| start_date_time | String  | 生産の開始日時です。指定した日時より後の履歴を抽出します。                                                                                                                                  |
| end_date_time   | String  | 生産の終了日時です。指定した日時より前の履歴を抽出します。未指定の場合、現在時刻より前の履歴を抽出します。                                                                                  |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:


### Response:

```json
{
    "jobstats": [
        {
            "machine_id": "M001",
            "file_name": "A1234567",
            "product_no": null,
            "start_date_time": "2021-10-29 17:10:02",
            "end_date_time": "2021-10-30 07:43:16",
            "qty_started": 156,
            "qty_finished": 120,
            "sewn_stitches": 164400,
            "cleanup_time": "00:00:00",
            "setup_time": "00:03:27",
            "sewing_time": "14:22:52",
            "running_time": "13:10:32",
            "total_error_time": "00:00:00",
            "thread_break_time": "00:00:00",
            "group_id_list": null,
            "group_name_list": null,
            "operator_id_list": [
                "UBE"
            ]
        },
        {
            "machine_id": "M001",
            "file_name": "A1234567",
            "product_no": null,
            "start_date_time": "2021-10-30 07:43:16",
            "end_date_time": "2021-10-30 09:13:50",
            "qty_started": 120,
            "qty_finished": 120,
            "sewn_stitches": 164400,
            "cleanup_time": "00:00:00",
            "setup_time": "00:03:27",
            "sewing_time": "01:23:40",
            "running_time": "00:11:18",
            "total_error_time": "00:00:00",
            "thread_break_time": "00:00:00",
            "group_id_list": [
                "G011"
            ],
            "group_name_list": [
                "New group"
            ],
            "operator_id_list": [
                "UBE"
            ]
        }
    ]
}
```

### Fields:

| Name              | Type    | Description                                                          |
| :---------------- | :------ | :------------------------------------------------------------------- |
| machine_id        | String  | ミシンIDです。                                                       |
| file_name         | String  | ファイル名です。                                                     |
| product_no        | String  | 生産番号です。                                                       |
| start_date_time   | String  | ジョブ開始日時です。                                                 |
| end_date_time     | String  | ジョブ完了日時です。（ジョブが継続している場合には集計日時）         |
| qty_started       | Integer | このジョブで開始した生産の総数です。                                 |
| qty_finished      | Integer | このジョブで完了した生産の総数です。                                 |
| sewn_stitches     | Integer | このジョブで実際に刺繍した総針数です。                               |
| cleanup_time      | String  | このジョブの後工程作業（刺繍完了後、運転セット解除まで）の時間です。 |
| setup_time        | String  | このジョブの準備作業（運転セット後、刺繍開始まで）の時間です。       |
| sewing_time       | String  | このジョブの刺繍作業（刺繍開始後、刺繍完了まで）の時間です。         |
| running_time      | String  | このジョブの刺繍作業時間のうち、ミシンが刺繍した時間です。           |
| total_error_time  | String  | このジョブのエラー時間です。                                         |
| thread_break_time | String  | このジョブのエラー時間のうち、上糸切れと下糸切れの時間です。         |
| group_id_list     | Array   | グループIDの配列です。                                               |
| group_name_list   | Array   | グループ名の配列です。                                               |
| operator_id_list  | Array   | オペレーターIDの配列です。                                           |

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 400  | 不正なクエリが指定されました。 |
| 404  | リソースが見つかりません。     |
| 500  | 内部でエラーが発生しました。   |

{% endapi %}
