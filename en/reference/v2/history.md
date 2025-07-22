# History


{% api "Get embroidery completion history", method="GET", url="/history/finished" %}

Get the embroidery completion history.Wildcards are allowed in some filters: "_" matches (1) character, " "matches many.

### Overview:

This endpoint returns a list of finished embroidery. You can filter the results using the following query parameters:
- Limited to specific sewing machines.
- Limited to specific operators.
- Limited to specific groups.
- Set the end time.
- Span/Interval setting. (default: 60min)

### Example:

**Get all embroidery completion history**

```
https://localhost/b-net/api/v2/history/finished?span=0
```

**Get the embroidery completion history for all machings with an IDs starting with M00**

```
https://localhost/b-net/api/v2/history/finished?machineID=M00_
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                                                    |
| :-------------- | :------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| machineID       | String  | Machine ID. Wildards allowed.                                                                                                                                                                                                  |
| operatorID      | String  | Operator ID. Wilcards allowed.                                                                                                                                                                                                 |
| groupName       | String  | Group name. Must be exact name.                                                                                                                                                                                                |
| designFilename  | String  | Design filename. Wildcard allowed.                                                                                                                                                                                             |
| fieldList       | String  | Specifies the value to return. Use in the form of "fieldList=field name" (e.g. "fieldList=machineID"). <br>Multiple fields can be specified by separating with commas (e.g. "fieldList=machineID, operatorID,designFilename"). |
| summarize       | String  | Specifies whether to report each run individually (false) or combine into a single record (True- Default).                                                                                                                     |
| span            | Number  | Instead of specifying a Start and End Date-time, this value specifies a time interval to report on, based on current time.                                                                                                     |
| startDateTime   | String  | Limit results to runs finished AFTER this date/time. Not valid with SPAN.                                                                                                                                                      |
| endDateTime     | String  | Limit results to runs finished BEFORE this date time. If not sepecified, defualts to current date/time.                                                                                                                        |
| pageSize        | Integer | The number of results per page.                                                                                                                                                                                                |
| pageOffset      | Integer | The page offset.                                                                                                                                                                                                               |
| sortOrder       | String  | The sort order of the results ("asc" or "desc").                                                                                                                                                                               |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name            | Type    | Description                                                   |
| :-------------- | :------ | :------------------------------------------------------------ |
| machineID       | String  | Embroidery machine ID.                                        |
| operatorID      | String  | Operator ID.                                                  |
| designFilename  | String  | Filename of stitch file on server, with no path or extension. |
| startDateTime   | String  | Start date/time.                                              |
| endDateTime     | String  | End date/time.                                                |
| qtyFinished     | Integer | Number of products completed.                                 |
| sewnStitches    | Integer | Total number of stitches sewn.                                |
| groupIDList     | Array   | Array listing Group ID's.                                     |
| groupNameList   | Array   | Array listing Group names.                                    |
| productionNo    | String  | Product number (from FDR3).                                   |


### Errors:

| Code | Description                           |
| :--- | :------------------------------------ |
| 204  | No content- no results to return.     |
| 400  | Bad request.                          |
| 401  | Authentication error.                 |
| 404  | Resource not found.                   |
| 409  | Resource contention.                  |
| 503  | Service not available (server error). |

{% endapi %}

{% api "Get Emboroider Error History", method="GET", url="/history/errors" %}

Get Embroidery machine error history.

### Overview:

Get embroidery error history. Wildcards are allowed in some filters: "_" matches (1) character, " "matches many. [ADD INFO IN CHART CURRENLTY IN NERVOUS MURDOCK：
- Limited to specific sewing machines.
- Limited to specific operators.
- Limited to specific groups.
- Set the end time.
- Span/Interval setting. (default: 60min)

### Example:

**Get all error occurrences**

```
https://localhost/b-net/api/v2/history/errors?span=0
```

**Get error occurrence history related to a specific design file**

```
https://localhost/b-net/api/v2/history/errors?designFilename=D013923
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                                                    |
| :-------------- | :------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| machineID       | String  | Machine ID. Wildards allowed.                                                                                                                                                                                                  |
| operatorID      | String  | Operator ID. Wilcards allowed.                                                                                                                                                                                                 |
| groupName       | String  | Group name. Must be exact name.                                                                                                                                                                                                |
| designFilename  | String  | Design filename. Wildcard allowed.                                                                                                                                                                                             |
| fieldList       | String  | Specifies the value to return. Use in the form of "fieldList=field name" (e.g. "fieldList=machineID"). <br>Multiple fields can be specified by separating with commas (e.g. "fieldList=machineID, operatorID,designFilename"). |
| span            | Number  | Instead of specifying a Start and End Date-time, this value specifies a time interval to report on, based on current time.                                                                                                     |
| startDateTime   | String  | Start date/time.                                                                                                                                                                                                               |
| endDateTime     | String  | End date/time.                                                                                                                                                                                                                 |
| pageSize        | Integer | The number of results per page.                                                                                                                                                                                                |
| pageOffset      | Integer | The page offset.                                                                                                                                                                                                               |
| sortOrder       | String  | The sort order of the results ("asc" or "desc").                                                                                                                                                                               |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name            | Type    | Description                                       |
| :-------------- | :------ | :------------------------------------------------ |
| machineID       | String  | Embroidery machine ID.                            |
| operatorID      | String  | Operator ID.                                      |
| designFilename  | String  | Design filename. Wildcard allowed.                |
| startDateTime   | String  | Date/time at start of error.                      |
| endDateTime     | String  | Date/time when error resolved.                    |
| eventCode       | String  | Event or Error code.                              |
| stitches        | Integer | Stitch number in the design where error occurred. |
| groupIDList     | Array   | Array listing Group ID's.                         |
| groupNameList   | Array   | Array listing Group names.                        |
| productionNo    | String  | Product number (from FDR3).                       |


### Errors:

| Code | Description                           |
| :--- | :------------------------------------ |
| 204  | No content- no results to return.     |
| 400  | Bad request.                          |
| 401  | Authentication error.                 |
| 404  | Resource not found.                   |
| 409  | Resource contention.                  |
| 503  | Service not available (server error). |

{% endapi %}

{% api "Get job completion history", method="GET", url="/history/jobstats" %}

Get job completion history.

### Overview:

Get job completion history. Wildcards are allowed in some filters: "_" matches (1) character, " "matches many：
- Limited to specific sewing machines.
- Limited to specific operators.
- Limited to specific groups.
- Set the end time.
- Span/Interval setting. (default: 60min)

### Example:

**Get all juob history**

```
https://localhost/b-net/api/v2/history/jobstats?span=0
```

**Get job history related to a specific job number**

```
https://localhost/b-net/api/v2/history/jobstats?productionNo=D013923
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                                                    |
| :-------------- | :------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| machineID       | String  | Machine ID. Wildards allowed.                                                                                                                                                                                                  |
| operatorID      | String  | Operator ID. Wilcards allowed.                                                                                                                                                                                                 |
| groupName       | String  | Group name. Must be exact name.                                                                                                                                                                                                |
| designFilename  | String  | Design filename. Wildcard allowed.                                                                                                                                                                                             |
| fieldList       | String  | Specifies the value to return. Use in the form of "fieldList=field name" (e.g. "fieldList=machineID"). <br>Multiple fields can be specified by separating with commas (e.g. "fieldList=machineID, operatorID,designFilename"). |
| productionNo    | String  | Product number (from FDR3).                                                                                                                                                                                                    |
| span            | Number  | Instead of specifying a Start and End Date-time, this value specifies a time interval to report on, based on current time.                                                                                                     |
| startDateTime   | String  | Limit results to runs finished AFTER this date/time. Not valid with SPAN.                                                                                                                                                      |
| endDateTime     | String  | Limit results to runs finished BEFORE this date time. If not sepecified, defualts to current date/time.                                                                                                                        |
| pageSize        | Integer | The number of results per page.                                                                                                                                                                                                |
| pageOffset      | Integer | The page offset.                                                                                                                                                                                                               |
| sortOrder       | String  | The sort order of the results ("asc" or "desc").                                                                                                                                                                               |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name              | Type    | Description                                                                      |
| :---------------- | :------ | :------------------------------------------------------------------------------- |
| machineID         | String  | Embroidery machine ID.                                                           |
| designFilename    | String  | Design filename.                                                                 |
| productionNo      | String  | Product number (from FDR3).                                                      |
| startDateTime     | String  | Job start date/time.                                                             |
| endDateTime       | String  | Job completed date/time. If job is still running, this will be the current time. |
| qtyStarted        | Integer | Number of products started.                                                      |
| qtyFinished       | Integer | Number of products completed.                                                    |
| sewnStitches      | Integer | Total number of stitches sewn.                                                   |
| cleanupTime       | String  | Total number of stitches sewn.                                                   |
| setupTime         | String  | Total Cleanup time.                                                              |
| sewingTime        | String  | Total time for this run.                                                         |
| runningTime       | String  | Total time with machine running.                                                 |
| totalErrorTime    | String  | Total Error Time.                                                                |
| threadBreakTime   | String  | Total Thread Break Time.                                                         |
| groupIDList       | Array   | Array listing Group ID's.                                                        |
| groupNameList     | Array   | Array listing Group names.                                                       |
| operatorIDList    | Array   | Array listing Operator ID's.                                                     |

### Errors:

| Code | Description                           |
| :--- | :------------------------------------ |
| 204  | No content- no results to return.     |
| 400  | Bad request.                          |
| 401  | Authentication error.                 |
| 404  | Resource not found.                   |
| 409  | Resource contention.                  |
| 503  | Service not available (server error). |

{% endapi %}
