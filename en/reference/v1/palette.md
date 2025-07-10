# Palette


{% api "Thread color palette registration", method="POST", url="/palette/threads" %}

Register the thread color palette.

### Example:

**Register the thread color palette.**

```
https://localhost/b-net/api/v1/palette/threads
```

### Query Parameters:

| Name | Type | Description              |
| :--- | :--- | :----------------------- |
| ---  | ---  | There are no parameters. |

### Request Headers:

| Header        | Description                        |
| :------------ | :--------------------------------- |
| authorization | API key set in B-NET Config.       |

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

| Name       | Type   | Description                                                                                       |
| :--------- | :----- | :------------------------------------------------------------------------------------------------ |
| serial     | String | The serial number.                                                                                |
| threadtype | String | It is a thread type.                                                                              |
| name       | String | The thread color name.                                                                            |
| rgb        | String | It is a thread color. A character string that cannot be converted to RGB will result in an error. |

### Response:

```json
{
    "result": "SUCCESS"
}
```

### Fields:

| Name   | Type   | Description                   |
| :----- | :----- | :---------------------------- |
| result | String | This is the execution result. |


### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

{% api "Thread color palette acquisition", method="GET", url="/palette/threads" %}

Get the thread color palette.

### Example:

**Get all thread colors (up to 500).**

```
https://localhost/b-net/api/v1/palette/threads
```

**Get the thread color of the thread type Angelking # 6 Half.**

```
https://localhost/b-net/api/v1/palette/threads?filter:threadtype=Angelking%20%236%20Half
```

**Get the thread color with thread color #FFFFFF.**

```
https://localhost/b-net/api/v1/palette/threads?filter:rgb=%23FFFFFF
```

### Query Parameters:

| Name     | Type    | Description                                                                                        |
| :------- | :------ | :------------------------------------------------------------------------------------------------- |
| per_page | Integer | The number of page data to get. Gets the information for the specified quantity.                   |
| page     | Integer | Optional offset If "per_page" is not blank. Starting value is 1. If ommitted, then the 1st page will be returned. For example, if per_page=10 and page=1, the 1st-10th machine's status will be returned. For page=2, machines 11-20 will be returned. |
| filter   | String  | It is a filter of the data to be acquired.                                                         |

### Filter:

| Name          | Type    | Description                                                                                                                                    |
| :------------ | :------ | :--------------------------------------------------------------------------------------------------------------------------------------------- |
| serial        | String  | The serial number of the thread color. You can use pattern matching.                                                                           |
| color         | String  | The thread color name. You can use pattern matching.                                                                                           |
| rgb           | String  | Thread color (RGB character string). You can use pattern matching.                                                                             |
| threadtype    | String  | It is a thread type. You can use pattern matching.                                                                                             |
| maxspeed      | Integer | The maximum number of revolutions.                                                                                                             |
| maxspeed_more | Integer | The maximum number of revolutions. Extracts thread information with the maximum number of revolutions that exceeds the specified value..       |
| maxspeed_less | Integer | The maximum number of revolutions. Extracts thread information with the maximum number of revolutions that does not meet the specified value.  |


### Request Headers:

| Header        | Description                        |
| :------------ | :--------------------------------- |
| authorization | API key set in B-NET Config.       |

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

| Name       | Type    | Description                          |
| :--------- | :------ | :----------------------------------- |
| palette_id | Integer | The palette ID.                      |
| serial     | String  | The serial number.                   |
| color      | String  | The thread color name.               |
| rgb        | String  | Thread color (RGB character string). |
| threadtype | String  | It is a thread type.                 |
| metadata   | JSON    | This is the metadata.                |


### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

{% api "Thread color palette deleted", method="DELETE", url="/palette/threads" %}

Delete the thread color palette. 

### Example:

**Delete the thread color of palette ID "12345".**

```
https://localhost/b-net/api/v1/palette/threads?palette_id=12345
```

### Query Parameters:

| Name       | Type    | Description                                   |
| :--------- | :------ | :-------------------------------------------- |
| palette_id | Integer | The palette ID. This is a required parameter. |

### Request Headers:

| Header        | Description                        |
| :------------ | :--------------------------------- |
| authorization | API key set in B-NET Config.       |

### Request Body:


### Response:

```json
{
    "result": "SUCCESS"
}
```

### Fields:

| Name   | Type   | Description                   |
| :----- | :----- | :---------------------------- |
| result | String | This is the execution result. |

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}
