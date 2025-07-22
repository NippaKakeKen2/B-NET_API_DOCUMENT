---
isTocVisible: true
---
# Machine

## Status
{% api "Get status information from one, several, or all machines. Optionally select which information to return", method="GET", url="/machine/status" %}

Get the status of the Embroidery machine.

### Example:

**Get the status of all Embroidery machines.**
```
https://localhost/b-net/api/v1/machine/status
```

**Get the status of the Embroidery machine with ID M001.**
```
https://localhost/b-net/api/v1/machine/status?filter:machine_id=M001
```

### Query Parameters:

| Name     | Type    | Description                                                                                                                                                                                                                                                                                                                                                      |
| :------- | :------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| per_page | Integer | (Optional) The number of machines values to return (page_size). If blank, all machines will be returned.                                                                                                                                                                                                                                                         |
| page     | Integer | Optional offset If "per_page" is not blank. Starting value is 1. If ommitted, then the 1st page will be returned. For example, if per_page=10 and page=1, the 1st-10th machine's status will be returned. For page=2, machines 11-20 will be returned.                                                                                                           |
| fields   | String  | List of fields to return. (optional) If not specified, all information will be returned. Multiple fields can be seperated by a comma. Uses field names as specified below. Example: "machineid,jcode".                                                                                                                                                           |
| order    | String  | Option to specify Sort Order for returned data. Can specify ASC (default) or DESC order, and multiple criteria. For example, "order = needle ASC, machineid DESC." Field names listed below  However, groupid, groupname cannot be used. The defualt sort order is "machineid ASC". Also note that some filters have comparison operators (exclude, more, less). |
| filter   | String  | Option to filter the data to be returned, based on the values in the returned fields. Some wildcards are available for pattern matchine. For example, "filter:machine_id=M%&needle=9" will return status of all 9 needle machines whose ID starts with M. The table of fileds below lists the filter information.                                                |


### Filter:

| Name                 | Type    | Description                                                                                                                                                |
| :------------------- | :------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------- |
| machine_id           | String  | The embroidery machine ID.  You can use pattern matching.                                                                                                  |
| jcode                | String  | Current Machine Event- include machines matching this event (Pattern Matching available).                                                                  |
| jcode_exc            | String  | EXCLUDE current machine Event- show machines that don't match this event (Pattern Matching available).                                                     |
| model                | String  | The model name. You can use pattern matching.                                                                                                              |
| operator_name        | String  | The operator name. Pattern matching is **not available**.                                                                                                  |
| operator_id          | String  | The operator ID. You can use pattern matching.                                                                                                             |
| design_name          | String  | Pattern name. You can use pattern matching.                                                                                                                |
| group_name           | String  | The group name. Pattern matching is **not available**.                                                                                                     |
| group_id             | String  | Group ID. You can use pattern matching.                                                                                                                    |
| head                 | Integer | The number of heads.                                                                                                                                       |
| needle               | Integer | The number of needle bars.                                                                                                                                 |
| needle_more          | Integer | The number of needle bars.                                                                                                                                 |
| needle_less          | Integer | The number of needle bars.                                                                                                                                 |
| remaining_time       | String  | Remaining work time. Specify in the "hour: minute: second" format.  Returns embroidery machines that match the specified time remaining.                   |
| remaining_time _more | String  | Greater than Remaining work time. Specify in the "hour: minute: second" format. Returns embroidery machines have more than the specified time remaining.   |
| remaining_time _less | String  | Less  than Remaining work time. Specify in the "hour: minute: second" format. Returns embroidery machines have less than the specified time remaining.     |

### Request Headers:

| Header        | Description                        |
| :------------ | :--------------------------------- |
| authorization | API key set in B-NET Config.       |

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

| Name                   | Type    | Description                                          |
| :--------------------- | :------ | :--------------------------------------------------- |
| machineid              | String  | The Embroidery machine ID.                           |
| model                  | String  | The model name.                                      |
| operatorid             | String  | The operator ID.                                     |
| operatorname           | String  | The operator name.                                   |
| head                   | Integer | The number of heads.                                 |
| effectivehead          | Integer | The number of effective heads.                       |
| errorheadtext          | String  | The error head position.                             |
| needle                 | Integer | The number of needle bars.                           |
| designname             | String  | The pattern name.                                    |
| designfullname         | String  | The full path of the pattern.                        |
| totalstitchcount       | String  | The total number of stitches on the pattern.         |
| sewingspeed            | Integer | Current machine speed.                               |
| machinesewingspeed     | Integer | Machine set embroidery speed.                        |
| jcode                  | String  | The status code.                                     |
| jcodealternativetext   | String  | Description of the status code.                      |
| currentstitchcount     | Integer | Current Stitch Number.                               |
| remainingtime          | String  | Amount of time left (estimated).                     |
| groupid                | String  | Group ID.                                            |
| groupname              | String  | The group name.                                      |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}


## Schedule

{% api "This endpoint adds a stitch file onto a machine's schedule.", method="POST", url="/machine/schedule" %}

The embroidery file is located on the BNET server's search path. This call has options to rename the stitch file (for example, to an order number) and to assign needles

### Example:

**Change the name of the file "ABC" to "DEF" and send it to the Embroidery machine "M001".**

```
https://localhost/b-net/api/v1/machine/schedule?machine_id=M001&file_name=ABC&output_name=DEF
```

**Rewrite the color change information of the file "ABC" to "C01, C02, C03" and send it to the Embroidery machine "M001".**

```
https://localhost/b-net/api/v1/machine/schedule?machine_id=M001&file_name=ABC&colors={"needles":[1,2,3]}
```

### Query Parameters:


| Name        | Type   | Description                                                                       |
| :---------- | :----- | :-------------------------------------------------------------------------------- |
| machine_id  | String | ID of the target embroidery machine (pattern matching not available).             |
| file_name   | String | Filename of stitch file on server, with no path or extension.                     |
| colors      | JSON   | Color Change Information- a JSON array of needles.                                |
| output_name | String | New file name at output.                                                          |
| job         | String | Write to the job table (t_jobs). <br>none：Nothing.<br>add：Add to the job table. |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

### Request Body:

### Response:

```json
{
    "file_name": "Number"
}
```

### Fields:

| Name      | Type   | Description                                                   |
| :-------- | :----- | :------------------------------------------------------------ |
| file_name | String | Filename of stitch file on server, with no path or extension. |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

{% api "This enpoint gets the current schedule of pending embroidery files for a specific machine, or for all machines", method="GET", url="/machine/schedule" %}

### Example:

**Get the schedule of Embroidery machine "M001".**

```
https://localhost/b-net/api/v1/machine/schedule?machine_id=M001
```

**Get the schedule for all Embroidery machines.**

```
https://localhost/b-net/api/v1/machine/schedule
```

### Query Parameters:

| Name       | Type    | Description                                                                                              |
| :--------- | :------ | :------------------------------------------------------------------------------------------------------- |
| machine_id | String  | ID of the target embroidery machine. (pattern matching not available).                                   |
| per_page   | Integer | (Optional) The number of values to return (page_size)  If blank, all will be returned.                   |
| page       | Integer | Optional offset If "per_page" is not blank. Starting value is 1. If ommitted, then the 1st page will be returned. For example, if per_page=10 and page=1, the 1st-10th machine's status will be returned. For page=2, machines 11-20 will be returned. |

### Request Headers:

| Header        | Description                        |
| :------------ | :--------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name      | Type   | Description                               |
| :-------- | :----- | :---------------------------------------- |
| machineid | String | The Embroidery machine ID.                |
| schedules | Array  | Embroidery Machine Schedule (JSON array). |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

{% api "This endpoint gets embroidery pattern information for a specific machine and schedule position", method="GET", url="/machine/schedule/design" %}

### Example:

**Get the pattern information for ths 1st design scheduled for machine "M001".**

```
https://localhost/b-net/api/v1/machine/schedule/design/?machine_id=M001&schedule_number=1
```

### Query Parameters:

| Name            | Type    | Description                                                                                  |
| :-------------- | :------ | :------------------------------------------------------------------------------------------- |
| machine_id      | String  | NOTE: What if pattern matching matches 2 machines? THIS SHOULD NOT ALLOW PATTERN MATCHING!.  |
| schedule_number | Integer | The schedule number. Numbers start at 1. This is a required parameter.                       |

### Request Headers:

| Header        | Description                        |
| :------------ | :--------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name                 | Type    | Description                                                   |
| :------------------- | :------ | :------------------------------------------------------------ |
| file_name            | String  | Filename of stitch file on server, with no path or extension. |
| stitches             | String  | The number of stitches.                                       |
| width                | String  | Width of pattern in 0.1mm.                                    |
| height               | String  | Height of pattern in 0.1mm.                                   |
| fdr3_root            | Integer | FDR3 and other information.                                   |
| fdr3_root/color_list | Integer | Color (Function List).                                        |
| fdr3_root/sewn_image | String  | Embroidery Image - JPEG- in base64.                           |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}


## Job

{% api "Job registration", method="POST", url="/machine/job" %}

Register the pattern assigned to the Embroidery machine (or the pattern to be assigned) in the job table (t_jobs). It is also possible to register patterns other than FDR3. 

### Example:


**Search the file "FLOWER" of the Embroidery machine "M001" and register it in the job table.**

```
https://localhost/b-net/api/v1/machine/job?machine_id=M001&file_name=FLOWER
```

### Query Parameters:

| Name       | Type   | Description                                                       |
| :--------- | :----- | :---------------------------------------------------------------- |
| machine_id | String | Full ID of Embroidery machine. Pattern matching is not available. |
| file_name  | String | Filename of stitch file on server, with no path or extension.     |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

### Request Body:


### Response:

```json
{
  "file_name": "Yacht",
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

| Name                 | Type    | Description                                                   |
| :------------------- | :------ | :------------------------------------------------------------ |
| file_name            | String  | Filename of stitch file on server, with no path or extension. |
| stitches             | String  | The number of stitches.                                       |
| width                | String  | Width of pattern in 0.1mm.                                    |
| height               | String  | Height of pattern in 0.1mm.                                   |
| fdr3_root            | Integer | FDR3 and other information.                                   |
| fdr3_root/color_list | Integer | Color (Function List).                                        |
| fdr3_root/sewn_image | String  | Embroidery Image - JPEG- in base64.                           |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

## Thread color

{% api "Thread color registration", method="POST", url="/machine/threads" %}

### Example:

**Register the thread color information of the Embroidery machine "M001".**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001
```

### Query Parameters:

| Name       | Type   | Description                                                       |
| :--------- | :----- | :---------------------------------------------------------------- |
| machine_id | String | Full ID of Embroidery machine. Pattern matching is not available. |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name       | Type    | Description                                                                                    |
| :--------- | :------ | :--------------------------------------------------------------------------------------------- |
| needle     | Integer | The needle bar number. This is a required parameter.                                           |
| serial     | String  | The serial number.                                                                             |
| threadtype | String  | The thread type.                                                                               |
| name       | String  | The thread color name.                                                                         |
| rgb        | String  | The thread color. A character string that cannot be converted to RGB will result in an error.  |
| maxspeed   | Integer | The maximum number of rotations.                                                               |
| memo       | String  | The Memo.                                                                                      |

### Response:

```json
{
    "result": "SUCCESS"
}
```

### Fields:

| Name   | Type   | Description           |
| :----- | :----- | :-------------------- |
| result | String | The execution result. |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

{% api "Thread color acquisition", method="GET", url="/machine/threads" %}

### Example:

**Acquire thread color information of Embroidery machine "M001".**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001
```

**Acquires thread color information for which the needle bar number of the Embroidery machine "M001" is greater than 1 and less than 5.**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001&filter:needle_number_more=1|needle_number_less=5
```

### Query Parameters:

| Name       | Type   | Description                                               |
| :--------- | :----- | :-------------------------------------------------------- |
| machine_id | String | Embroidery machine ID. Pattern matching is not available. |
| filter     | String | Filter of the data to be acquired.                        |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

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

| Name         | Type    | Description                            |
| :----------- | :------ | :------------------------------------- |
| needlenumber | Integer | The needle bar number.                 |
| serial       | String  | The serial number.                     |
| threadtype   | String  | The thread type.                       |
| color        | String  | Thread color name.                     |
| rgb          | String  | RGB of the thread color.               |
| status       | Integer | It is in the state of thread stand.    |
| metadata     | JSON    | This is the metadata.                  |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

{% api "Thread color deletion", method="DELETE", url="/machine/threads" %}

### Example:

**Delete the thread color information of Embroidery machine "M001".**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001
```

**Acquire thread color information of needle bar 2 of Embroidery machine "M001".**

```
https://localhost/b-net/api/v1/machine/threads?machine_id=M001&needle_number=2
```


### Query Parameters:

| Name          | Type    | Description                                                                             |
| :------------ | :------ | :-------------------------------------------------------------------------------------- |
| machine_id    | String  | Embroidery machine ID. Pattern matching is not available. This is a required parameter. |
| needle_number | Integer | The needle bar number. If not specified, all needle bars will be deleted.               |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

### Request Body:


### Response:

```json
{
    "result": "SUCCESS"
}
```

### Fields:

| Name   | Type   | Description           |
| :----- | :----- | :-------------------- |
| result | String | The execution result. |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

