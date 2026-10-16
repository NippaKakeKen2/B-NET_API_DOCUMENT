# Orders


{% api "Order Information Retrieval", method="GET", url="/orders" %}

Retrieves order information.

### OVERVIEW:

Returns an array of order data from the order table (t_orders) that matches the filter parameters. Can return 3 levels of information- full, brief, or status only. Please note that the t_orders has one row for each embroidery to be sewn, and is identified by task_id which is typically the barcode used in direct download. For scheduled download, this might be ORDER_ID & LINE_NO & LINE_LOCATION

### Example:

**Retrieve all order information in a concise format**

```
https://localhost/b-net/api/v2/orders?detail=brief
```

**Retrieve complete order information for a specific order ID**

```
https://localhost/b-net/api/v2/orders?orderID=CO&detail=full
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                         |
| :-------------- | :------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| taskID          | String  | Unique identifier for this embroidery file to be sewn.                                                                                                                              |
| detail          | String  | Determines the amount of information returned.                                                                                                                                      |
| orderID         | String  | Filter by specific order ID.                                                                                                                                                        |
| batchID         | String  | Filter by batch ID.                                                                                                                                                                 |
| customerNo      | String  | Filter by specific customer ID.                                                                                                                                                     |
| status          | String  | Order status filter: 'all' (default), 'unfinished', 'C' (completed).                                                                                                                |
| dueStartDateTime| String  | Start date: filters orders with due dates after the specified date.                                                                                                                 |
| dueEndDateTime  | String  | End date: filters orders with due dates before the specified date.                                                                                                                  |
| pageSize        | Integer | Number of results per page.                                                                                                                                                         |
| pageOffset      | Integer | Page offset.                                                                                                                                                                        |
| sortOrder       | String  | Sort order of results ("asc" or "desc")                                                                                                                                             |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | API key configured in B-NET Config |

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

Depending on the detail level returned, the following fields may be included:

| Name               | Type    | Description                                |
| :----------------- | :------ | :----------------------------------------- |
| taskID             | String  | Item barcode ID (primary key)              |
| orderID            | String  | Order ID                                   |
| orderLN            | Integer | Line number                                |
| orderLNLoc         | String  | Location                                   |
| orderDate          | String  | Order date                                 |
| productSheets      | String  | Product sheet                              |
| customerNo         | String  | Customer number                            |
| customerName       | String  | Customer name                              |
| department         | String  | Department                                 |
| status             | String  | Order status                               |
| comboType          | String  | Combo Type (future)                        |
| parentTaskID       | String  | Parent Task ID (future)                    |
| qty                | Integer | Total Quantity to sew                      |
| qtyFinished        | Integer | Completed quantity                         |
| qtyDamaged         | Integer | Damaged quantity                           |
| due                | String  | Due Date (date or date/time formatted string) |
| tags               | String  | Tags (strings array)                       |
| batchID            | String  | Batch ID                                   |
| designFilename     | String  | Pattern file name (on server)              |
| designFolder       | String  | Subfolder to search in                     |
| designPath         | String  | Where the file file is located on the server, when file is validated. |
| designFolderAlias  | String  | Folder Alias (set in BNET CONFIG.          |
| designFileStatus   | String  | file vaildation status                     |
| designFileStatusDate | String | Date validated                            |
| colorway           | String  | ID of colorway to use (future)             |
| colorAssign        | String  | JSON map of colors to stops, or colors to needles |
| colorList          | String  | array of color values used                 |
| frame              | String  | name of frame                              |
| colors             | Integer | Number of colors used in design            |
| stops              | Integer | Number of stops                            |
| stitches           | Integer | total stitches                             |
| width              | Integer | width in 1/10mm                            |
| height             | Integer | height in 1/10 mm                          |
| estRuntime         | String  | Estimated sewing time                      |
| creatorInfo        | String  | Creator information                        |
| fdr3Info           | String  | FDR3 information                           |
| prjInfo            | String  | PRJ information                            |
| itemSKU            | String  | Item SKU                                   |
| itemName           | String  | Item name                                  |
| sizeColorChart     | String  | Size/Color/QTY chart                       |
| comments           | String  | Comments or Memo                           |
| userT1             | String  | User text 1                                |
| userT2             | String  | User text 2                                |
| userN1             | Number  | User number 1                              |
| userD1             | String  | User date 1                                | 

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | No content                     |
| 400  | Bad request                    |
| 401  | Authentication error           |
| 404  | Resource not found             |
| 409  | Resource conflict              |
| 503  | Service unavailable            |

{% endapi %}

{% api "Order Registration", method="POST", url="/orders" %}

Registers orders into the order table (t_orders).

### OVERVIEW:

Add a list of orders to the t_orders table.  This is a JSON array of one or more JSON order objects. Required paramaters are taskID, orderID, dueDate, qty, and designFilename.

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | API key configured in B-NET Config |

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
| taskID             | String  | Item barcode ID (primary key)              |
| orderID            | String  | Order ID                                   |
| orderLN            | Integer | Line number                                |
| orderLNLoc         | String  | Location                                   |
| orderDate          | String  | Order date                                 |
| productSheets      | String  | Product sheet                              |
| customerNo         | String  | Customer number                            |
| customerName       | String  | Customer name                              |
| department         | String  | Department                                 |
| status             | String  | Order status                               |
| comboType          | String  | Combo Type (future)                        |
| parentTaskID       | String  | Parent Task ID (future)                    |
| qty                | Integer | Total Quantity to sew                      |
| qtyFinished        | Integer | Completed quantity                         |
| qtyDamaged         | Integer | Damaged quantity                           |
| due                | String  | Due Date (date or date/time formatted string) |
| tags               | String  | Tags (Strings array)                       |
| batchID            | String  | Batch ID                                   |
| designFilename     | String  | Pattern file name (on server)              |
| designFolder       | String  | Subfolder to search in                     |
| designPath         | String  | Where the file file is located on the server, when file is validated. |
| designFolderAlias  | String  | Folder Alias (set in BNET CONFIG.          |
| designFileStatus   | String  | file vaildation status                     |
| designFileStatusDate | String | Date validated                            |
| colorway           | String  | ID of colorway to use (future)             |
| colorAssign        | String  | JSON map of colors to stops, or colors to needles |
| colorList          | String  | array of color values used                 |
| frame              | String  | name of frame                              |
| colors             | Integer | Number of colors used in design            |
| stops              | Integer | Number of stops                            |
| stitches           | Integer | total stitches                             |
| width              | Integer | width in 1/10mm                            |
| height             | Integer | height in 1/10 mm                          |
| estRuntime         | String  | Estimated sewing time                      |
| creatorInfo        | String  | Creator information                        |
| fdr3Info           | String  | FDR3 information                           |
| prjInfo            | String  | PRJ information                            |
| itemSKU            | String  | Item SKU                                   |
| itemName           | String  | Item name                                  |
| sizeColorChart     | String  | Size/Color/QTY chart                       |
| comments           | String  | Comments or Memo                           |
| userT1             | String  | User text 1                                |
| userT2             | String  | User text 2                                |
| userN1             | Number  | User number 1                              |
| userD1             | String  | User date 1                                | 

### Response:

```json
{
  "result": "SUCCESS"
}
```

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | No content                     |
| 400  | Bad request                    |
| 401  | Authentication error           |
| 404  | Resource not found             |
| 409  | Resource conflict              |
| 503  | Service unavailable            |

{% endapi %}

{% api "Order Update", method="PUT", url="/orders" %}

Updates one or more orders in the order table (t_orders).

### OVERVIEW:

This endpoint is used to modify data in T_ORDERS. Typical uses are to cancel an order, note quantity damaged, change quantity. Normally done one row at a time, however, the due date ofor an entire order or batch may be changed. 

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | API key configured in B-NET Config |

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
| taskID             | String  | Item barcode ID (primary key)              |
| orderID            | String  | Order ID                                   |
| orderLN            | Integer | Line number                                |
| orderLNLoc         | String  | Location                                   |
| orderDate          | String  | Order date                                 |
| productSheets      | String  | Product sheet                              |
| customerNo         | String  | Customer number                            |
| customerName       | String  | Customer name                              |
| department         | String  | Department                                 |
| status             | String  | Order status                               |
| comboType          | String  | Combo Type (future)                        |
| parentTaskID       | String  | Parent Task ID (future)                    |
| qty                | Integer | Total Quantity to sew                      |
| qtyFinished        | Integer | Completed quantity                         |
| qtyDamaged         | Integer | Damaged quantity                           |
| due                | String  | Due Date (date or date/time formatted string) |
| tags               | String  | Tags (Strings array)                       |
| batchID            | String  | Batch ID                                   |
| designFilename     | String  | Pattern file name (on server)              |
| designFolder       | String  | Subfolder to search in                     |
| designPath         | String  | Where the file file is located on the server, when file is validated. |
| designFolderAlias  | String  | Folder Alias (set in BNET CONFIG.          |
| designFileStatus   | String  | file vaildation status                     |
| designFileStatusDate | String | Date validated                            |
| colorway           | String  | ID of colorway to use (future)             |
| colorAssign        | String  | JSON map of colors to stops, or colors to needles |
| colorList          | String  | array of color values used                 |
| frame              | String  | name of frame                              |
| colors             | Integer | Number of colors used in design            |
| stops              | Integer | Number of stops                            |
| stitches           | Integer | total stitches                             |
| width              | Integer | width in 1/10mm                            |
| height             | Integer | height in 1/10 mm                          |
| estRuntime         | String  | Estimated sewing time                      |
| creatorInfo        | String  | Creator information                        |
| fdr3Info           | String  | FDR3 information                           |
| prjInfo            | String  | PRJ information                            |
| itemSKU            | String  | Item SKU                                   |
| itemName           | String  | Item name                                  |
| sizeColorChart     | String  | Size/Color/QTY chart                       |
| comments           | String  | Comments or Memo                           |
| userT1             | String  | User text 1                                |
| userT2             | String  | User text 2                                |
| userN1             | Number  | User number 1                              |
| userD1             | String  | User date 1                                | 

### Response:

```json
{
  "result": "SUCCESS"
}
```

### Errors:

| Code | Description                    |
| :--- | :----------------------------- |
| 204  | No content                     |
| 400  | Bad request                    |
| 401  | Authentication error           |
| 404  | Resource not found             |
| 409  | Resource conflict              |
| 503  | Service unavailable            |

{% endapi %}

{% api "Order Deletion", method="DELETE", url="/orders" %}

Deletes one or more order data entries from the order table (t_orders).

### OVERVIEW:

This endpoint deletes one or more order data entries from the order table.

### Example:

**Delete specific order data**

```
https://localhost/b-net/api/v2/orders
```

### Request Headers:

| Header           | Description                                   |
| :--------------- | :-------------------------------------------- |
| authorization    | API key configured in B-NET Config            |
| orderID          | Order ID to delete (e.g., CO-1001)            |
| taskID           | Task ID to delete (e.g., CO-1001_1)           |
| batchID          | Batch ID to delete (e.g., 2024-01-16 Wave 01) |
| status           | Status to delete (e.g., C - Completed, F - Finished, X - Cancelled, P - Pending, H - On Hold) |

※ When multiple deletion items are specified simultaneously, only order data matching all specified items will be deleted.

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
| 204  | No content                     |
| 400  | Bad request                    |
| 401  | Authentication error           |
| 404  | Resource not found             |
| 409  | Resource conflict              |
| 503  | Service unavailable            |

{% endapi %}