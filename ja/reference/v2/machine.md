# Machine（ミシン）

## スケジュール

{% api "スケジュールの取得", method="GET", url="/machine/schedule-items" %}

指定したミシンの未送信スケジュールを取得します。


### 概要:

このエンドポイントは、指定したミシンに現在セットされている未送信スケジュール（柄ファイルの一覧）と、その内容を表すハッシュ値を返します。

`schedule` の並び順は、ミシンへ送信される順番です。

返される `scheduleHash` は、スケジュールの更新（`PUT`）や削除（`DELETE`）を行う際に必要です。取得後にスケジュールが変化していないかを確認するために使用されます。

### Example:

**ミシンID KS001 のスケジュールを取得する**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001
```

**ミシンIDに記号を含む場合（KS001+002）**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001%2B002
```

### Query Parameters:

| Name      | Type   | Description                                                                                          |
| :-------- | :----- | :--------------------------------------------------------------------------------------------------- |
| machineID | String | **必須**。ミシンIDです。完全一致で検索します。`+` や空白を含む場合は URL エンコードしてください（`+` → `%2B`、空白 → `%20`）。 |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Response:

```json
{
    "scheduleHash": "sha256:978f53cacff533dfa68cfec6e1764752cc9c57c93bb6f2fe7d7ad26b7e45ce23",
    "schedule": [
        "Design\\ABCDEFG(21259)\\ABCDEFG.PRJ",
        "Design\\BARUDAN(17039)\\BARUDAN.PRJ"
    ],
    "modifiedBy": "Polling",
    "lastModifiedUtc": "2026-09-29T07:37:23Z"
}
```

### Fields:

| Name            | Type   | Description                                                                                                   |
| :-------------- | :----- | :------------------------------------------------------------------------------------------------------------ |
| scheduleHash    | String | スケジュールの内容を表すハッシュ値です（`sha256:` + 16進数64桁）。柄の追加・削除・並び順の変更で値が変わります。 |
| schedule        | Array  | 未送信の柄ファイルパスの配列です。ミシンごとの柄保存フォルダからの相対パスで、配列の順番が送信順です。         |
| modifiedBy      | String | 最後にスケジュールを変更した処理です。<br>・`Polling`：ポーリングによる自動変換<br>・`DFS-INIT`：DFSによる初期化 |
| lastModifiedUtc | String | 最後にスケジュールが変更された日時です（UTC、ISO 8601 形式）。                                               |

### 注意事項:

- `scheduleHash` は、パスの大文字・小文字、区切り文字（`/` と `\`）の違いを区別せずに計算されます。
- JSON の仕様により、パス区切りの `\` はレスポンス上では `\\` と表記されます。

### Errors:

| Code | Description                                          |
| :--- | :--------------------------------------------------- |
| 204  | コンテンツなし。指定したミシンのスケジュールが空です。 |
| 400  | 不正なリクエスト。`machineID` が指定されていません。   |
| 401  | 認証エラー。                                         |
| 404  | リソースが見つかりません。指定したミシンIDが存在しません。 |
| 503  | サービス利用不可。                                   |

{% endapi %}

{% api "スケジュールの更新", method="PUT", url="/machine/schedule-items" %}

指定したミシンの未送信スケジュールを、送信した内容で置き換えます。

### 概要:

このエンドポイントは、指定したミシンの未送信スケジュールを、リクエストボディの `schedule` 配列の内容と順番で置き換えます。スケジュールの並び替え、柄の追加・削除に使用します。

事前に `GET /machine/schedule-items` で取得した `scheduleHash` を指定する必要があります。取得後にスケジュールが変化している場合（他の操作による変更や、ミシンへの送信によって柄が減った場合など）は、`409` が返され更新は行われません。

**このエンドポイントは更新要求を受け付けるものです。** ミシンへの反映は B-NET 本体が非同期で行います。反映結果は `GET /machine/schedule-items` で `scheduleHash` を確認してください。

### Example:

**ミシンID KS001 のスケジュールを並び替える**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53cacff533dfa68cfec6e1764752cc9c57c93bb6f2fe7d7ad26b7e45ce23
```

### Query Parameters:

| Name         | Type   | Description                                                                 |
| :----------- | :----- | :-------------------------------------------------------------------------- |
| machineID    | String | **必須**。ミシンIDです。                                                    |
| scheduleHash | String | **必須**。`GET /machine/schedule-items` で取得した `scheduleHash` の値です。 |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |
| Content-Type  | `application/json`             |

### Request Body:

```json
{
    "schedule": [
        "Design\\BARUDAN(17039)\\BARUDAN.PRJ",
        "Design\\ABCDEFG(21259)\\ABCDEFG.PRJ"
    ]
}
```

### Request Body Parameters:

| Name     | Type  | Description                                                                                             |
| :------- | :---- | :------------------------------------------------------------------------------------------------------ |
| schedule | Array | 新しいスケジュールです。柄ファイルパスを送信順に並べた配列で、形式は `GET` の `schedule` と同じです。空の配列を指定すると、未送信スケジュールがすべて削除されます。 |

### Response:

```json
{
    "result": "SUCCESS"
}
```

### 注意事項:

- `schedule` に指定した柄ファイルが 1 件でも見つからない場合、スケジュール全体が更新されません（一部だけが反映されることはありません）。
- ミシンへ柄を送信中の場合、送信完了後に反映されます。送信によってスケジュールが変化した場合は反映されません。`GET` で取得し直してから再度実行してください。
- パス区切りの `\` は JSON の仕様に従い `\\` とエスケープしてください。
- 文字コードは UTF-8 です。

### Errors:

| Code | Description                                                                 |
| :--- | :-------------------------------------------------------------------------- |
| 400  | 不正なリクエスト。必須パラメータがない、またはリクエストボディが JSON として不正です。 |
| 401  | 認証エラー。                                                                |
| 404  | リソースが見つかりません。指定したミシンIDが存在しません。                  |
| 409  | リソースの競合。`scheduleHash` が現在のスケジュールと一致しません（Schedule has changed）。 |
| 503  | サービス利用不可。                                                          |

{% endapi %}

{% api "スケジュールの削除", method="DELETE", url="/machine/schedule-items" %}

指定したミシンの未送信スケジュールから柄を削除します。

### 概要:

このエンドポイントは、指定したミシンの未送信スケジュールから、条件に一致する柄を削除します。削除条件は `all`、`ordinal`、`filePath`、`fileName` のうち **1 つだけ** 指定します。

事前に `GET /machine/schedule-items` で取得した `scheduleHash` を指定する必要があります。取得後にスケジュールが変化している場合は `409` が返され、削除は行われません。

**このエンドポイントは削除要求を受け付けるものです。** ミシンへの反映は B-NET 本体が非同期で行います。

### Example:

**すべての柄を削除する**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53...&all
```

**1 番目と 3 番目の柄を削除する**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53...&ordinal=1,3
```

**パスを指定して削除する**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53...&filePath=Design%5CABCDEFG(21259)%5CABCDEFG.PRJ
```

**ファイル名を指定して削除する（拡張子は省略可）**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53...&fileName=ABCDEFG
```

### Query Parameters:

| Name         | Type   | Description                                                                                                 |
| :----------- | :----- | :---------------------------------------------------------------------------------------------------------- |
| machineID    | String | **必須**。ミシンIDです。                                                                                    |
| scheduleHash | String | **必須**。`GET /machine/schedule-items` で取得した `scheduleHash` の値です。                                 |
| all          | -      | 値は不要です。未送信スケジュールの柄をすべて削除します。                                                    |
| ordinal      | String | 削除する柄の番号です（1 始まり、`GET` で取得した `schedule` の順番）。カンマ区切りで複数指定できます（例: `1,3`）。 |
| filePath     | String | 削除する柄ファイルのパスです。`GET` の `schedule` と同じ形式で指定します。一致する柄をすべて削除します。     |
| fileName     | String | 削除する柄のファイル名です。拡張子は省略できます。一致する柄をすべて削除します。                           |

※ `filePath` と `fileName` は、大文字・小文字と区切り文字（`/` と `\`）の違いを区別しません。<br>
※ `\` や日本語、`+` を含む値は URL エンコードしてください。<br>

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Response:

```json
{
    "result": "SUCCESS"
}
```

### Fields:

| Name    | Type   | Description                  |
| :------ | :----- | :--------------------------- |
| result  | String | 処理結果です。               |

### Errors:

| Code | Description                                                                                       |
| :--- | :------------------------------------------------------------------------------------------------ |
| 204  | コンテンツなし。指定したミシンのスケジュールが空です。                                             |
| 400  | 不正なリクエスト。<br>・One of filePath, all, fileName, or ordinal is required：削除条件が指定されていません<br>・Only one of filePath, all, fileName, or ordinal can be specified：削除条件が複数指定されています<br>・条件に一致する柄がない、または `ordinal` が範囲外です |
| 401  | 認証エラー。                                                                                      |
| 404  | リソースが見つかりません。指定したミシンIDが存在しません。                                        |
| 409  | リソースの競合。`scheduleHash` が現在のスケジュールと一致しません（Schedule has changed）。          |
| 503  | サービス利用不可。                                                                                |

{% endapi %}
