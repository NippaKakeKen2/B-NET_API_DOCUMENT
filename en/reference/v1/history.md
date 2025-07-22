# History


{% api "Get history of FINISHED PRODUCTS", method="GET", url="/history?type=finished" %}

Lists completed embroidery statistics for given criteria rangs. Some paramaters accept wildcards.

### Example:

**Get all completed embroidery statistics (max 500)**

```
https://localhost/b-net/api/v1/history?type=finished
```

**Get embroidery statistics for all machines whose ID starts with "M00"**

```
https://localhost/b-net/api/v1/history?type=finished&machine_id=M00_
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                 |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type            | String  | Specifies type of history. (finished, error, or jobstats)                                                                                                                                   |
| per_page        | Integer | Specifies number of results to return per page.                                                                                                                                             |
| page            | Integer | Specifies Page Offset. This is 1 based. Example: per_page=10. For page=1, data will be runs 1-10.                                                                                           |
| machine_id      | String  | Filter on Machine ID. Wilcdards "_" or "???" allowed.                                                                                                                                       |
| operator_id     | String  | Filter on Operator ID. Wilcdards "_" or "???" allowed.                                                                                                                                      |
| group_id        | String  | Filter on Group ID. No wildcards.                                                                                                                                                           |
| group_name      | String  | Filter on Group Name. No wildcards.                                                                                                                                                         |
| file_name       | String  | Filter on File Name. Wildcards allowed.                                                                                                                                                     |
| production_no   | String  | Filter on Production Number (fromFDR3) Wildcards allowed.                                                                                                                                   |
| start_date_time | String  | Start date time. Limit results to runs completed after this date time.                                                                                                                      |
| end_date_time   | String  | Finish date time. Limite results to runs completed before this date/time. If no value specified, will show all data up till present time.                                                   |


### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name            | Type    | Description                                                   |
| :-------------- | :------ | :------------------------------------------------------------ |
| machine_id      | String  | The Embroidery machine ID.                                    |
| operator_id     | String  | The operator ID.                                              |
| file_name       | String  | Filename of stitch file on server, with no path or extension. |
| start_date_time | String  | Emboridery run starting date time.                            |
| end_date_time   | String  | Emboridery run finished date time.                            |
| qty_finished    | Integer | Number of pieces produced.                                    |
| sewn_stitches   | Integer | Total number of stitches.                                     |
| group_id_list   | Array   | Array of Group ID's that this was run on.                     |
| group_name_list | Array   | Array of Group Names that this was run on.                    |
| product_no      | String  | Production Number. (FDR3)                                     |


### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 400  | Illegal query specified.          |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

{% api "Get Error History", method="GET", url="/history?type=errors" %}

Get error history, filterable by time period, machine name, etc.

### Example:

**Get all error history (max 500)**

```
https://localhost/b-net/api/v1/history?type=errors
```

**Get all errors with Event Code D16**

```
https://localhost/b-net/api/v1/history?type=errors&event_code=D16
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                 |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type            | String  | Specifies type of history. (finished, error, or jobstats)                                                                                                                                   |
| per_page        | Integer | Specifies number of results to return per page.                                                                                                                                             |
| page            | Integer | Specifies Page Offset. This is 1 based. Example: per_page=10. For page=1, data will be runs 1-10.                                                                                           |
| machine_id      | String  | Filter on Machine ID. Wilcdards "_" or "???" allowed.                                                                                                                                       |
| operator_id     | String  | Filter on Operator ID. Wilcdards "_" or "???" allowed.                                                                                                                                      |
| group_id        | String  | Filter on Group ID. No wildcards.                                                                                                                                                           |
| group_name      | String  | Filter on Group Name. No wildcards.                                                                                                                                                         |
| file_name       | String  | Filter on File Name. Wildcards allowed.                                                                                                                                                     |
| production_no   | String  | Filter on Production Number. (fromFDR3) Wildcards allowed.                                                                                                                                  |
| start_date_time | String  | Start date time. Limit results to errors occuring after this date time.                                                                                                                     |
| end_date_time   | String  | Finish date time. Limite results to errors occuring before this date/time. If no value specified, will show all data up till present time.                                                  |
| event_code      | String  | Filter on this error event code. Wildcards allowed.                                                                                                                                         |


### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name            | Type   | Description                                                   |
| :-------------- | :----- | :------------------------------------------------------------ |
| machine_id      | String | The Embroidery machine ID.                                    |
| operator_id     | String | The operator ID.                                              |
| file_name       | String | Filename of stitch file on server, with no path or extension. |
| start_date_time | String | Emboridery run starting date time.                            |
| end_date_time   | String | Emboridery run finished date time.                            |
| event_code      | String | Event Code.                                                   |
| group_id_list   | Array  | Array of Group ID's that this was run on.                     |
| group_name_list | Array  | Array of Group Names that this was run on.                    |
| product_no      | String | Production Number. (FDR3)                                     |


### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 400  | Illegal query specified.          |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

{% api "Get JOB history", method="GET", url="/history?type=jobstats" %}

Get Job history, filterable.

### Example:

**Get All Jobs (500 max)**

```
https://localhost/b-net/api/v1/history?type=jobstats
```

**Get all jobs with operatorID="UBE"**

```
https://localhost/b-net/api/v1/history?type=jobstats&operator_id="UBE"
```

### Query Parameters:

| Name            | Type    | Description                                                                                                                                                                                 |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type            | String  | Specifies type of history. (finished, error, or jobstats)                                                                                                                                   |
| per_page        | Integer | Specifies number of results to return per page.                                                                                                                                             |
| page            | Integer | Specifies Page Offset. This is 1 based. Example: per_page=10. For page=1, data will be runs 1-10.                                                                                           |
| machine_id      | String  | Filter on Machine ID. Wilcdards "_" or "???" allowed.                                                                                                                                       |
| operator_id     | String  | Filter on Operator ID. Wilcdards "_" or "???" allowed.                                                                                                                                      |
| group_id        | String  | Filter on Group ID. No wildcards.                                                                                                                                                           |
| group_name      | String  | Filter on Group Name. No Wildcards.                                                                                                                                                         |
| file_name       | String  | Filter on File Name. Wildcards allowed.                                                                                                                                                     |
| production_no   | String  | Filter on Production Number (fromFDR3) Wildcards allowed.                                                                                                                                   |
| start_date_time | String  | Start date time. Limit results to runs completed after this date time.                                                                                                                      |
| end_date_time   | String  | Finish date time. Limite results to runs completed before this date/time. If no value specified, will show all data up till present time.                                                   |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name              | Type    | Description                                                                                                                   |
| :---------------- | :------ | :---------------------------------------------------------------------------------------------------------------------------- |
| machine_id        | String  | The Embroidery machine ID.                                                                                                    |
| file_name         | String  | Filename of stitch file on server, with no path or extension.                                                                 |
| product_no        | String  | Production Number. (FDR3)                                                                                                     |
| start_date_time   | String  | Starting date/time for job.                                                                                                   |
| end_date_time     | String  | Finishing date for job.<br>(If the job is still ongoing (not finished yet), date is in event date time that happened latest.) |
| qty_started       | Integer | Number of pieces started.                                                                                                     |
| qty_finished      | Integer | Number of pieces finished.                                                                                                    |
| sewn_stitches     | Integer | Total number of stitches.                                                                                                     |
| cleanup_time      | String  | Amount of time spent between runs- post process.                                                                              |
| setup_time        | String  | Amount of time spent in Preperation.                                                                                          |
| sewing_time       | String  | Elapsed time spent running this job- start to finish.                                                                         |
| running_time      | String  | Amount of time spent actively running.                                                                                        |
| total_error_time  | String  | Amount of time spent fixing all errors.                                                                                       |
| thread_break_time | String  | Amount of time spent repairing thread break stoppage.                                                                         |
| group_id_list     | Array   | Array of Group ID's that this was run on.                                                                                     |
| group_name_list   | Array   | Array of Group Names that this was run on.                                                                                    |
| operator_id_list  | Array   | Array of operator ID's running this job.                                                                                      |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 400  | Illegal query specified.          |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}
