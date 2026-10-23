# Machine（ミシン）

## スケジュール

{% api "Get the schedule", method="GET", url="/machine/schedule-items" %}

Retrieves the unsent schedules for the specified embroidery machine.


### 概要:

This endpoint returns the list of unsent schedules (design files) currently set on the specified embroidery machine, along with hash values representing their contents.

The `schedule` order represents the order in which the schedules will be sent to the embroidery machine.

The returned `scheduleHash` is required when updating (`PUT`) or deleting (`DELETE`) a schedule. It is used to verify that the schedule has not changed since it was retrieved.

### Example:

**Retrieve the schedule for machine ID KS001**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001
```

**When the machine ID contains special characters (KS001+002)**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001%2B002
```

### Query Parameters:

| Name      | Type   | Description                                                                                          |
| :-------- | :----- | :--------------------------------------------------------------------------------------------------- |
| machineID | String | **Required**. The machine ID. An exact match is used for the search. If the ID contains `+` or spaces, URL-encode them (`+` → `%2B`, space → `%20`). |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | API key set in B-NET Config |

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
| scheduleHash    | String | A hash value representing the contents of the schedule (`sha256:`: followed by 64 hexadecimal digits). The value changes when a design is added or deleted, or when the order of the designs is changed. |
| schedule        | Array  | An array of file paths for unsent design files. The paths are relative to the design storage folder for each machine, and the order of the array represents the order in which the designs will be sent.         |
| modifiedBy      | String | The process that most recently modified the schedule.<br>-`Polling`: Automatic conversion by polling.<br>-`DFS-INIT`: Initialization by DFS |
| lastModifiedUtc | String | The date and time when the schedule was last modified (UTC, ISO 8601 format).                                               |

### Notes:

- The `scheduleHash` is calculated without distinguishing between uppercase and lowercase letters in the paths or between path separators (`/` and `\`).
- Due to the JSON specification, the path separator `\` is represented as `\\` in the response.

### Errors:

| Code | Description                                          |
| :--- | :--------------------------------------------------- |
| 204  | No content. The schedule for the specified machine is empty. |
| 400  | Invalid request. `machineID` is not specified.   |
| 401  | Authentication error.                                         |
| 404  | Resource not found. The specified machine ID does not exist. |
| 503  | Service is no available.                                   |

{% endapi %}

{% api "Update the schedule", method="PUT", url="/machine/schedule-items" %}

Replaces the unsent schedule for the specified machine with the submitted schedule.

### 概要:

This endpoint replaces the unsent schedule for the specified machine with the contents and order of the `schedule` array in the request body. It is used to reorder, add, or delete designs.

The `scheduleHash` obtained in advance from `GET /machine/schedule-items` must be specified. If the schedule has changed since it was retrieved (for example, due to another operation or because a design was sent to the machine and removed from the schedule), a `409` response is returned and the schedule is not updated.

**This endpoint accepts schedule update requests.**  The update is applied to the machine asynchronously by the B-NET application. To verify that the update has been applied, check the `scheduleHash` using `GET /machine/schedule-items`.
### Example:

**Reorder the schedule for machine ID KS001**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53cacff533dfa68cfec6e1764752cc9c57c93bb6f2fe7d7ad26b7e45ce23
```

### Query Parameters:

| Name         | Type   | Description                                                                 |
| :----------- | :----- | :-------------------------------------------------------------------------- |
| machineID    | String | **Required**. The machine ID.                                                    |
| scheduleHash | String | **Required**. The `scheduleHash` value obtained from `GET /machine/schedule-items` |

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | API key set in B-NET Config |
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
| schedule | Array | The new schedule. An array of design file paths in the order they will be sent, using the same format as the `schedule` returned by `GET`. Specifying an empty array removes all unsent schedules. |

### Response:

```json
{
    "result": "SUCCESS"
}
```

### Notes:

- If even one of the design files specified in `schedule` cannot be found, the entire schedule is not updated. Partial updates are not performed.
- If designs are currently being sent to the machine, the update is applied after the transmission is completed. If the schedule has changed as a result of the transmission, the update is not applied. Retrieve the schedule again using `GET` and retry the request.
- Escape the path separator `\` as `\\` in accordance with the JSON specification.
- The character encoding is UTF-8.

### Errors:

| Code | Description                                                                 |
| :--- | :-------------------------------------------------------------------------- |
| 400  | Invalid request. A required parameter is missing, or the request body contains invalid JSON. |
| 401  | Authentication error.                                                                |
| 404  | Resource not found. The specified machine ID does not exist.                  |
| 409  | Resource conflict. The `scheduleHash` does not match the current schedule (Schedule has changed). |
| 503  | Service is no available.                                                          |

{% endapi %}

{% api "Delete the schedule", method="DELETE", url="/machine/schedule-items" %}

Removes a design from the unsent schedule of the specified machine.

### 概要:

This endpoint removes designs matching the specified condition from the unsent schedule of the specified machine. Exactly one of the following deletion criteria must be specified: `all`, `ordinal`, `filePath`, or `fileName`.

The  `scheduleHash`  obtained in advance from `GET /machine/schedule-items`  must be specified. If the schedule has changed since it was retrieved, a 409 response is returned and the deletion is not performed.

**This endpoint accepts deletion requests.** The deletion is applied to the machine asynchronously by the B-NET application.

### Example:

**Delete all designs**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53...&all
```

**Delete the 1st and 3rd designs**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53...&ordinal=1,3
```

**Delete by specifying the file path**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53...&filePath=Design%5CABCDEFG(21259)%5CABCDEFG.PRJ
```

**Delete by specifying the file name (extension optional)**

```
https://localhost/b-net/api/v2/machine/schedule-items?machineID=KS001&scheduleHash=sha256:978f53...&fileName=ABCDEFG
```

### Query Parameters:

| Name         | Type   | Description                                                                                                 |
| :----------- | :----- | :---------------------------------------------------------------------------------------------------------- |
| machineID    | String | **Required**. The machine ID.                                                                                    |
| scheduleHash | String | **Required**. The scheduleHash value obtained from GET /machine/schedule-items.                                 |
| all          | -      | No value is required. Deletes all designs from the unsent schedule.                                                    |
| ordinal      | String | The ordinal numbers of the designs to delete (1-based, corresponding to the order of the `schedule` returned by `GET`). Multiple values can be specified as comma-separated numbers (e.g., `1,3`). |
| filePath     | String | The file path of the design to delete. Specify it in the same format as the `schedule` returned by `GET`. All matching designs are deleted.     |
| fileName     | String | The file name of the design to delete. The file extension can be omitted. All matching designs are deleted.                           |

※ `filePath` and `fileName` are case-insensitive and do not distinguish between path separators (`/` and `\`).<br>
※ Values containing `\`, Japanese characters, or `+` must be URL-encoded.<br>

### Request Headers:

| Header        | Description                    |
| :------------ | :----------------------------- |
| authorization | API key set in B-NET Config |

### Response:

```json
{
    "result": "SUCCESS"
}
```

### Fields:

| Name    | Type   | Description                  |
| :------ | :----- | :--------------------------- |
| result  | String | Processing result               |

### Errors:

| Code | Description                                                                                       |
| :--- | :------------------------------------------------------------------------------------------------ |
| 204  | No content. The schedule for the specified machine is empty.                                             |
| 400  | Invalid request.<br>- No deletion criterion is specified.<br>- Multiple deletion criteria are specified.<br>- No matching designs were found, or `ordinal` is out of range. |
| 401  | Authentication error.                                                                                      |
| 404  | Resource not found. The specified machine ID does not exist.                                        |
| 409  | Resource conflict. The `scheduleHash` does not match the current schedule (Schedule has changed).          |
| 503  | Service is no available.                                                                                |

{% endapi %}
