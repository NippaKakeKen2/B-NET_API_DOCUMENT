---
isTocVisible: true
---
# Design


{% api "Preservation of embroidery pattern", method="POST", url="/design" %}

Search for the embroidery pattern and save it in the specified folder. 

### Example:

**Search the API Searching folder for the file "ABC" and save it in the API Queue folder on your server.**

```
https://localhost/b-net/api/v1/design?file_name=ABC
```

**Search the API Searching folder for the file "ABC" and save it in the subfolder "temp" of the server's API Queue folder.**

```
https://localhost/b-net/api/v1/design?file_name=ABC&folder=temp
```

**Search the API Searching folder for the file "ABC", rename it to "DEF" and save it in the API Queue folder on your server.**

```
https://localhost/b-net/api/v1/design?file_name=ABC&output_name=DEF
```

**Search the file "ABC" from the API Searching folder, rewrite the color change information to "C01, C02, C03" and save it in the API Queue folder of the server.**

```
https://localhost/b-net/api/v1/design?file_name=ABC&colors={"needles":[1,2,3]}
```

### Query Parameters:

| Name        | Type   | Description                                                                                                                                                     |
| :---------- | :----- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| file_name   | String | The name of the file to search..                                                                                                                                |
| folder      | String | The output destination after searching. Specifies the relative path of the API Queue folder. If not specified, it will be saved in the API Queue folder.        |
| colors      | Array  | Color change information.                                                                                                                                       |
| output_name | String | The file name to output.                                                                                                                                        |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

### Request Body:


### Response:

```json
{
    "file_name": [
        "123456789"
    ]
}
```

### Fields:

| Name      | Type  | Description                 |
| :-------- | :---- | :-------------------------- |
| file_name | Array | The saved file name.        |


### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}


{% api "Pattern information acquisition", method="GET", url="/design/info" %}

Gets the pattern registered in the job table (t_jobs). Embroidery images cannot be obtained. 

### Example:

**Get the information of file "ZZ" from the job table.**

```
https://localhost/b-net/api/v1/design/info?file_name=ZZ
```

### Query Parameters:

| Name      | Type    | Description                                                                                              |
| :-------- | :------ | :------------------------------------------------------------------------------------------------------- |
| file_name | String  | The file name. You can use pattern matching. This is a required parameter.                               |
| per_page  | Integer | The number of page data to get. Acquires the pattern information for the specified quantity.             |
| page      | Integer | Optional offset If "per_page" is not blank. Starting value is 1. If ommitted, then the 1st page will be returned. For example, if per_page=10 and page=1, the 1st-10th machine's status will be returned. For page=2, machines 11-20 will be returned. |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

### Request Body:


### Response:

```json
[
    {
        "filename": "ZZ",
        "stitches": 1371,
        "width": 1103,
        "height": 216,
        "fdr3_root": {
            "color_list": [
                {
                    "stitch": 1,
                    "function": "C04"
                },
                {
                    "stitch": 103,
                    "function": "C03"
                }
            ]
        }
    }
]
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

### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}


{% api "Upload embroidery design", method="POST", url="/design/upload" %}

Upload the embroidery pattern and save it in the specified folder.  

### Example:

**Upload the file "ABC.DST" and save it in the API Queue folder on the server.**

```
https://localhost/b-net/api/v1/design/upload?file_name=ABC.DST
```

**Upload the file "ABC.DST" and save it in the subfolder "temp" of the API Queue folder on the server.**

```
https://localhost/b-net/api/v1/design/upload?file_name=ABC.DST&folder=temp
```

### Query Parameters:

| Name      | Type   | Description                                                                                                                                                |
| :-------- | :----- | :--------------------------------------------------------------------------------------------------------------------------------------------------------- |
| file_name | String | The file name and extension to upload. It supports Barudan format and Tajima format.                                                                       |
| folder    | String | The output destination after uploading. Specifies the relative path of the API Queue folder. If not specified, it will be saved in the API Queue folder.   |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

### Request Body:

```json
{
  "design_file": "Base64 design binary ..."
}

```

### Response:

```json
{
    "file_name": [
        "ABC"
    ]
}
```

### Fields:

| Name      | Type  | Description                 |
| :-------- | :---- | :-------------------------- |
| file_name | Array | The saved file name.        |


### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}

