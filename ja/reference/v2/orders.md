# Orders（オーダー）


{% api "オーダー状態の取得（非推奨）", method="GET", url="/orders/status" %}

オーダー状態を取得します。このエンドポイントは非推奨です。

### 概要:

このエンドポイントは、フィルターパラメータに一致するオーダーデータの配列をオーダーテーブル（t_orders）から返します。

**注意：このエンドポイントは非推奨です**

### Example:

**特定のオーダーIDのオーダー状態を取得する**

```
https://localhost/b-net/api/v2/orders/status?orderID=Testfile.U01
```

**特定の期間内の納期を持つオーダー状態を取得する**

```
https://localhost/b-net/api/v2/orders/status?dueStartDateTime=2023-11-01T09:12:28Z&dueEndDateTime=2023-11-30T09:12:28Z
```

### Query Parameters:

| Name            | Type    | Description                                                                                                       |
| :-------------- | :------ | :---------------------------------------------------------------------------------------------------------------- |
| orderID         | String  | 特定のオーダーIDでフィルタリングします                                                                           |
| batchID         | String  | バッチのIDでフィルタリングします                                                                                 |
| customerNo      | String  | 特定の顧客のIDでフィルタリングします                                                                             |
| status          | String  | オーダー状態フィルター。'all'（デフォルト）、'unfinished'、'C'（完了）など                                       |
| dueStartDateTime| String  | 開始日時。指定した日時以降の納期を持つオーダーをフィルタリングします                                             |
| dueEndDateTime  | String  | 終了日時。指定した日時以前の納期を持つオーダーをフィルタリングします                                             |
| pageSize        | Integer | 1ページあたりの結果数です                                                                                         |
| pageOffset      | Integer | ページオフセットです                                                                                              |
| sortOrder       | String  | 結果のソート順です（"asc"または"desc"）                                                                          |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Response:

```json
[
  {
    "taskID": "CO2",
    "orderID": "CO-1002",
    "orderLN": "1",
    "customerNo": "C-1001",
    "customerName": "Barudan America, Inc.",
    "department": "monogramming",
    "status": "R",
    "qty": "1",
    "due": "2024-02-24 02:32:28",
    "comboType": "P",
    "parentTaskID": "Batch0001",
    "batchID": "2024-01-16 Wave 01"
  },
  {
    "taskID": "CO9",
    "orderID": "CO9",
    "orderLN": "1",
    "customerNo": "C-1001",
    "customerName": "Barudan America, Inc.",
    "department": "monogramming",
    "status": "R",
    "qty": "100",
    "due": "2024-02-24 02:32:28",
    "comboType": "P",
    "parentTaskID": "Batch0001",
    "batchID": "2024-01-16 Wave 01"
  }
]
```

### Fields:

| Name             | Type    | Description                                |
| :--------------- | :------ | :----------------------------------------- |
| taskID           | String  | アイテムのバーコードID（主キー）           |
| orderID          | String  | オーダーID                                 |
| orderLN          | String  | ライン番号                                 |
| orderLNLoc       | String  | ロケーション                               |
| batchID          | String  | バッチID                                   |
| status           | String  | オーダー状態                               |
| designFileStatus | String  | 柄ファイルの状態                     |
| orderDate        | String  | 注文日                                     |
| dueDate          | String  | 納期                                       |
| qty              | String  | 数量                                       |
| qtyFinished      | String  | 完了数量                                   |
| qtyDamaged       | String | 破損数量                                   |

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | コンテンツなし                 |
| 400  | 不正なリクエスト               |
| 401  | 認証エラー                     |
| 404  | リソースが見つかりません       |
| 409  | リソースの競合                 |
| 503  | サービス利用不可               |

{% endapi %}

{% api "オーダー情報の取得", method="GET", url="/orders" %}

オーダー情報を取得します。

### 概要:

このエンドポイントは、フィルターパラメータに一致するオーダーデータの配列をオーダーテーブル（t_orders）から返します。

### Example:

**すべてのオーダー情報を簡潔な形式で取得する**

```
https://localhost/b-net/api/v2/orders?detail=brief
```

**特定のオーダーIDのオーダー情報を完全な形式で取得する**

```
https://localhost/b-net/api/v2/orders?orderID=CO&detail=full
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                         |
| :-------------- | :------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| detail          | String  | 返される情報の量を決定します。<br>・brief：TaskID、OrderID/LN、CustomerStatus、Qty、Due、BatchID<br>・status：TaskID、Status、Qty、QtyFinished、QtyDamaged<br>・full：完全な情報 |
| orderID         | String  | 特定のオーダーIDでフィルタリングします                                                                                                                                             |
| batchID         | String  | バッチのIDでフィルタリングします                                                                                                                                                   |
| customerNo      | String  | 特定の顧客のIDでフィルタリングします                                                                                                                                               |
| status          | String  | オーダー状態フィルター。'all'（デフォルト）、'unfinished'、'C'（完了）など                                                                                                         |
| dueStartDateTime| String  | 開始日時。指定した日時以降の納期を持つオーダーをフィルタリングします                                                                                                               |
| dueEndDateTime  | String  | 終了日時。指定した日時以前の納期を持つオーダーをフィルタリングします                                                                                                               |
| pageSize        | Integer | 1ページあたりの結果数です                                                                                                                                                           |
| pageOffset      | Integer | ページオフセットです                                                                                                                                                                |
| sortOrder       | String  | 結果のソート順です（"asc"または"desc"）                                                                                                                                            |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Response:

```json
[
  {
    "taskID": "CO2",
    "orderID": "CO-1002",
    "orderLN": "1",
    "orderLNLoc": "1",
    "orderDate": "2024-02-24 02:32:28",
    "productSheets": "{Myorder.PDF,Myorder.JPG1}",
    "customerNo": "C-1001",
    "customerName": "Barudan America, Inc.",
    "department": "monogramming",
    "status": "R",
    "comboType": "P",
    "parentTaskID": "Batch0001",
    "qty": "1",
    "qtyFinished": "0",
    "qtyDamaged": "0",
    "due": "2024-02-24 02:32:28",
    "tags": "{Metallic,Multi-head,LargeField,HighValue}",
    "batchID": "2024-01-16 Wave 01",
    "designFilename": "Test",
    "designFolder": "cap",
    "designPath": "",
    "designFolderAlias": "",
    "designFileStatus": " ",
    "designFileStatusDate": "2024-02-24 02:32:28",
    "colorway": "Colorway01",
    "colorAssign": "{\"mapStopToThreadID\":[\"918-1801\",\"918-1722\",\"!STOP!\"]}",
    "colorList": "[\"1875\",\"1801\",\"1675\"]",
    "frame": "string",
    "colors": "1",
    "stops": "2",
    "stitches": "3",
    "width": "10",
    "height": "20",
    "estRuntime": "{\"time\":\"00:32:28\"}",
    "creatorInfo": "{\"name\":\"User\"}",
    "fdr3Info": "{\"fdr3Data\":{\"version\":1,\"productionID\":\"312-01\",\"qty\":1,\"speedStart\":900,\"speedMax\":1100,\"frameName\":\"18cm Blue Round\",\"frameOutlineName\":\"18CM50\",\"backing\":\"2 layers of solvy.\",\"position\":\"Left Pocket\",\"operator\":\"robert\",\"memo\":\"Sew, trim & bag\",\"due\":\"1\\/1\\/2022\",\"frameInfo\":\"1,2,3,4,5,6\",\"areaDesignName\":\"AcmeCorporateLogo\"},\"fdr3Palette\":{\"version\":1,\"firstStitch\":\"1\",\"backgroundColor\":\"0xFFFFFF\",\"threads\":[{\"needle\":\"1\",\"color\":\"C01\",\"serial\":\"1801\",\"name\":\"White\",\"threadType\":\"Madeira Polyneon\",\"maxSpeed\":\"500\",\"RGB\":\"#FEFEFE\"},{\"needle\":-1,\"color\":\"C02\",\"serial\":\"1800\",\"name\":\"Black\",\"threadType\":\"Madeira Polyneon\",\"RGB\":\"#010101\"},{\"needle\":-1,\"color\":\"C03\",\"serial\":\"1755\",\"name\":\"Red\",\"threadType\":\"Madeira Polyneon\",\"RGB\":\"#800000\"}]}}",
    "prjInfo": "{\"vScale\":200,\"hScale\":105,\"rotPattern\":2,\"angle\":0,\"origin\":1,\"socks\":0,\"applique\":0,\"aHoffset\":0,\"aVoffset\":0,\"frameout\":0,\"fHoffset\":0,\"fVoffset\":0,\"capframe\":0,\"frametype\":0,\"repeat\":1,\"matrix\":0,\"vRepeat\":1,\"hRepeat\":1,\"vSpace\":0,\"hSpace\":0,\"startDir\":0,\"swingType\":0,\"p23\":0,\"p24\":0,\"p25\":0,\"p26\":0,\"p27\":0,\"p28\":0,\"p29\":0,\"frmOffsetH\":0,\"frmOffsetV\":0,\"frmP1H\":0,\"frmP1V\":0,\"frmP2H\":0,\"frmP2V\":0}",
    "itemSKU": "string",
    "itemName": "string",
    "sizeColorChart": null,
    "comments": "string",
    "userT1": "string",
    "userT2": "string",
    "userN1": "0",
    "userD1": "2024-02-24 02:32:28"
  }
]
```

### Fields:

返される詳細レベルに応じて、以下のフィールドが含まれます：

| Name               | Type    | Description                                |
| :----------------- | :------ | :----------------------------------------- |
| taskID             | String  | アイテムのバーコードID（主キー）           |
| orderID            | String  | オーダーID                                 |
| orderLN            | Integer | ライン番号                                 |
| orderLNLoc         | String  | ロケーション                               |
| orderDate          | String  | 注文日                                     |
| productSheets      | String  | 製品シート                                 |
| customerNo         | String  | 顧客番号                                   |
| customerName       | String  | 顧客名                                     |
| department         | String  | 部門                                       |
| status             | String  | オーダー状態                               |
| comboType          | String  | コンボタイプ                               |
| parentTaskID       | String  | 親タスクID                                 |
| qty                | Integer | 数量                                       |
| qtyFinished        | Integer | 完了数量                                   |
| qtyDamaged         | Integer | 破損数量                                   |
| due                | String  | 納期                                       |
| tags               | String  | タグ                                       |
| batchID            | String  | バッチID                                   |
| designFilename     | String  | 柄ファイル名                         |
| designFolder       | String  | 柄フォルダ                           |
| designPath         | String  | 柄パス                               |
| designFolderAlias  | String  | 柄フォルダエイリアス                 |
| designFileStatus   | String  | 柄ファイル状態                       |
| designFileStatusDate | String | 柄ファイル状態更新日                 |
| colorway           | String  | カラーウェイ                               |
| colorAssign        | String  | 色割り当て                                 |
| colorList          | String  | 色リスト                                   |
| frame              | String  | フレーム                                   |
| colors             | Integer | 色数                                       |
| stops              | Integer | ストップ数                                 |
| stitches           | Integer | ステッチ数                                 |
| width              | Integer | 幅                                         |
| height             | Integer | 高さ                                       |
| estRuntime         | String  | 推定実行時間                               |
| creatorInfo        | String  | 作成者情報                                 |
| fdr3Info           | String  | FDR3情報                                   |
| prjInfo            | String  | PRJ情報                           |
| itemSKU            | String  | アイテムSKU                                |
| itemName           | String  | アイテム名                                 |
| sizeColorChart     | String  | カラーチャート                              |
| comments           | String  | コメント                                   |
| userT1             | String  | ユーザーテキスト1                          |
| userT2             | String  | ユーザーテキスト2                          |
| userN1             | Number  | ユーザー数値1                              |
| userD1             | String  | ユーザー日付1                              | 

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | コンテンツなし                 |
| 400  | 不正なリクエスト               |
| 401  | 認証エラー                     |
| 404  | リソースが見つかりません       |
| 409  | リソースの競合                 |
| 503  | サービス利用不可               |

{% endapi %}

{% api "オーダーの登録", method="POST", url="/orders" %}

オーダーをBNETデータベース（t_orders）に登録します。

### 概要:

このエンドポイントは、新しいオーダーのJSONリストをT_ORDERSデータベースに追加します。

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:

```json
[
  {
    "taskID": "CO1",
    "orderID": "CO-1001",
    "orderLN": "1",
    "orderLNLoc": "1",
    "orderDate": "2024-02-23T17:32:28Z",
    "productSheets": [
      "Myorder.PDF",
      "Myorder.JPG1"
    ],
    "customerNo": "C-1001",
    "customerName": "Barudan America, Inc.",
    "department": "monogramming",
    "comboType": "P",
    "parentTaskID": "Batch0001",
    "qty": 1,
    "qtyFinished": 0,
    "qtyDamaged": 0,
    "due": "2024-02-23T17:32:28Z",
    "tags": "Metallic, Multi-head, LargeField, HighValue",
    "batchID": "2024-01-16 Wave 01",
    "designFilename": "Test",
    "designFolder": "cap",
    "designFileStatus": "",
    "designPath": "",
    "designFolderAlias": "",
    "designFileStatusDate": "2024-02-23T17:32:28Z",
    "colorway": "Colorway01",
    "colorAssign": { "mapStopToThreadID": [ "918-1801", "918-1722", "!STOP!"]},
    "colorList": ["1875","1801","1675"],
    "frame": "string",
    "colors": 1,
    "stops": 2,
    "stitches": 3,
    "width": 10,
    "height": 20,
    "estRuntime": {"time":"00:32:28"},
    "creatorInfo": {"name": "User"},
    "fdr3Info": {"fdr3Data": {"version": 1,"productionID": "312-01","qty": 1,"speedStart": 900,"speedMax": 1100,"frameName": "18cm Blue Round","frameOutlineName":"18CM50","backing": "2 layers of solvy.","position": "Left Pocket","operator": "robert","memo": "Sew, trim & bag","due": "1/1/2022","frameInfo": "1,2,3,4,5,6","areaDesignName": "AcmeCorporateLogo","image": "<IMAGE>" },"fdr3Palette": {"version": 1,"firstStitch": "1","backgroundColor": "0xFFFFFF",
    "threads": [{"needle": "1","color": "C01","serial": "1801","name": "White","threadType": "Madeira Polyneon","maxSpeed": "500","RGB": "#FEFEFE"   },{"needle": -1,"color": "C02","serial": "1800","name": "Black","threadType": "Madeira Polyneon","RGB": "#010101" },{ "needle": -1,"color": "C03","serial": "1755","name": "Red","threadType": "Madeira Polyneon","RGB": "#800000"}]}},
    "prjInfo": {"vScale": 200,"hScale": 105,"rotPattern": 2,"angle": 0,"origin": 1,"socks": 0,"applique": 0,"aHoffset": 0,"aVoffset": 0,"frameout": 0,"fHoffset": 0,"fVoffset": 0,"capframe": 0,"frametype": 0,"repeat": 1,"matrix": 0,"vRepeat": 1,"hRepeat": 1,"vSpace": 0,"hSpace": 0,"startDir": 0,"swingType": 0,"p23": 0,"p24": 0,"p25": 0,"p26": 0,"p27": 0,"p28": 0,"p29": 0,"frmOffsetH": 0,"frmOffsetV": 0,"frmP1H": 0,"frmP1V": 0,"frmP2H": 0,"frmP2V": 0},
    "itemSKU": "string",
    "itemName": "string",
    "sizeColorChart": {},
    "comments": "string",
    "userT1": "string",
    "userT2": "string",
    "userN1": 0,
    "userD1": "2024-02-23T17:32:28Z"
  }
]
```

### Request Body Parameters:

| Name               | Type    | Description                                |
| :----------------- | :------ | :----------------------------------------- |
| taskID             | String  | アイテムのバーコードID（主キー）           |
| orderID            | String  | オーダーID                                 |
| orderLN            | Integer | ライン番号                                 |
| orderLNLoc         | String  | ロケーション                               |
| orderDate          | String  | 注文日                                     |
| productSheets      | String  | 製品シート                                 |
| customerNo         | String  | 顧客番号                                   |
| customerName       | String  | 顧客名                                     |
| department         | String  | 部門                                       |
| status             | String  | オーダー状態                               |
| comboType          | String  | コンボタイプ                               |
| parentTaskID       | String  | 親タスクID                                 |
| qty                | Integer | 数量                                       |
| qtyFinished        | Integer | 完了数量                                   |
| qtyDamaged         | Integer | 破損数量                                   |
| due                | String  | 納期                                       |
| tags               | String  | タグ                                       |
| batchID            | String  | バッチID                                   |
| designFilename     | String  | 柄ファイル名                         |
| designFolder       | String  | 柄フォルダ                           |
| designPath         | String  | 柄パス                               |
| designFolderAlias  | String  | 柄フォルダエイリアス                 |
| designFileStatus   | String  | 柄ファイル状態                       |
| designFileStatusDate | String | 柄ファイル状態更新日                 |
| colorway           | String  | カラーウェイ                               |
| colorAssign        | String  | 色割り当て                                 |
| colorList          | String  | 色リスト                                   |
| frame              | String  | フレーム                                   |
| colors             | Integer | 色数                                       |
| stops              | Integer | ストップ数                                 |
| stitches           | Integer | ステッチ数                                 |
| width              | Integer | 幅                                         |
| height             | Integer | 高さ                                       |
| estRuntime         | String  | 推定実行時間                               |
| creatorInfo        | String  | 作成者情報                                 |
| fdr3Info           | String  | FDR3情報                                   |
| prjInfo            | String  | PRJ情報                           |
| itemSKU            | String  | アイテムSKU                                |
| itemName           | String  | アイテム名                                 |
| sizeColorChart     | String  | カラーチャート                              |
| comments           | String  | コメント                                   |
| userT1             | String  | ユーザーテキスト1                          |
| userT2             | String  | ユーザーテキスト2                          |
| userN1             | Number  | ユーザー数値1                              |
| userD1             | String  | ユーザー日付1                              | 

### Response:

```json
{
  "result": "SUCCESS"
}
```

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | コンテンツなし                 |
| 400  | 不正なリクエスト               |
| 401  | 認証エラー                     |
| 404  | リソースが見つかりません       |
| 409  | リソースの競合                 |
| 503  | サービス利用不可               |

{% endapi %}

{% api "オーダーの更新", method="PUT", url="/orders" %}

オーダーテーブル（t_orders）内の1つ以上のオーダーを更新します。

### 概要:

このエンドポイントは、通常、数量、破損、納期などを変更するために使用されます。通常、一度に1つのオーダー、オーダーライン、またはオーダーラインロケーションを変更するために使用されますが、バッチ全体の納期を更新する必要がある場合もあります。

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | B-NET Config で設定したAPIキー |

### Request Body:

```json
[
  {
    "taskID": "CO-1001_1",
    "qty": 10,
    "qtyFinished": 10,
    "due": "2024-02-23T17:32:28Z",
    "designFileStatusDate": "2024-03-23T17:32:28Z"
  }
]
```

### Request Body Parameters:

| Name               | Type    | Description                                |
| :----------------- | :------ | :----------------------------------------- |
| taskID             | String  | アイテムのバーコードID（主キー）           |
| orderID            | String  | オーダーID                                 |
| orderLN            | Integer | ライン番号                                 |
| orderLNLoc         | String  | ロケーション                               |
| orderDate          | String  | 注文日                                     |
| productSheets      | String  | 製品シート                                 |
| customerNo         | String  | 顧客番号                                   |
| customerName       | String  | 顧客名                                     |
| department         | String  | 部門                                       |
| status             | String  | オーダー状態                               |
| comboType          | String  | コンボタイプ                               |
| parentTaskID       | String  | 親タスクID                                 |
| qty                | Integer | 数量                                       |
| qtyFinished        | Integer | 完了数量                                   |
| qtyDamaged         | Integer | 破損数量                                   |
| due                | String  | 納期                                       |
| tags               | String  | タグ                                       |
| batchID            | String  | バッチID                                   |
| designFilename     | String  | 柄ファイル名                         |
| designFolder       | String  | 柄フォルダ                           |
| designPath         | String  | 柄パス                               |
| designFolderAlias  | String  | 柄フォルダエイリアス                 |
| designFileStatus   | String  | 柄ファイル状態                       |
| designFileStatusDate | String | 柄ファイル状態更新日                 |
| colorway           | String  | カラーウェイ                               |
| colorAssign        | String  | 色割り当て                                 |
| colorList          | String  | 色リスト                                   |
| frame              | String  | フレーム                                   |
| colors             | Integer | 色数                                       |
| stops              | Integer | ストップ数                                 |
| stitches           | Integer | ステッチ数                                 |
| width              | Integer | 幅                                         |
| height             | Integer | 高さ                                       |
| estRuntime         | String  | 推定実行時間                               |
| creatorInfo        | String  | 作成者情報                                 |
| fdr3Info           | String  | FDR3情報                                   |
| prjInfo            | String  | PRJ情報                           |
| itemSKU            | String  | アイテムSKU                                |
| itemName           | String  | アイテム名                                 |
| sizeColorChart     | String  | カラーチャート                              |
| comments           | String  | コメント                                   |
| userT1             | String  | ユーザーテキスト1                          |
| userT2             | String  | ユーザーテキスト2                          |
| userN1             | Number  | ユーザー数値1                              |
| userD1             | String  | ユーザー日付1                              | 

### Response:

```json
{
  "result": "SUCCESS"
}
```

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | コンテンツなし                 |
| 400  | 不正なリクエスト               |
| 401  | 認証エラー                     |
| 404  | リソースが見つかりません       |
| 409  | リソースの競合                 |
| 503  | サービス利用不可               |

{% endapi %}

{% api "オーダーの削除", method="DELETE", url="/orders" %}

T_ORDERSデータベースから1つ以上のオーダーを削除します。

### 概要:

このエンドポイントは、BNET T_Ordersから1つ以上のオーダーエントリを削除します。

### Example:

**特定のオーダーリストを削除する**

```
https://localhost/b-net/api/v2/orders
```

### Request Headers:

| Header           | Description                                   |
| :--------------- | :-------------------------------------------- |
| authorization    | B-NET Config で設定したAPIキー |
| orderList        | 削除するオーダーIDの配列（例: ["CO-1001", "CO-1002"]）|
| batchID          | 削除するバッチID（例: 2024-01-16 Wave 01）     |

### Response:

```json
{
  "result": "SUCCESS",
  "deletedCount": 5
}
```

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | コンテンツなし                 |
| 400  | 不正なリクエスト               |
| 401  | 認証エラー                     |
| 404  | リソースが見つかりません       |
| 409  | リソースの競合                 |
| 503  | サービス利用不可               |

{% endapi %}