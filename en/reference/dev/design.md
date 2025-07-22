---
isTocVisible: true
---
# Design


{% api "Upload embroidery file to BNET", method="POST", url="/design" %}

Upload an embroidery file - in BASE64; can apply FDR3 paramaters, and including file name, in a specified subfolder, and set needles/colors.

### Example:

**Upload the file (base64 in the body) and name it "ABC." Will be saved to the folder specified as API Queue in BNET Config**

```
https://localhost/b-net/api/dev/design?file_name=ABC
```

### Query Parameters:

| Name      | Type   | Description                                                                                                |
| :-------- | :----- | :--------------------------------------------------------------------------------------------------------- |
| file_name | String | Name to save the file under.                                                                               |
| folder    | String | Optional subfolder underneath API Queue. If ommited, will be saved in API Queue.                           |

### Request Headers:

| Header        | Description                                    |
| :------------ | :--------------------------------------------- |
| authorization | API key for authorization. Set in BNET Config. |

### Request Body:

```json
{
    "fdr3": {
        "product_number": "312-01",
        "item_name": "item#1",
        "product_type": "A",
        "qty": 1,
        "speed_start": 1000,
        "speed_max": 1100,
        "frame_name": "18cm Blue Round",
        "frame_outline_name": "18CM50",
        "backing_type": "2 layers of solvy.",
        "where_to_sew": "Left Pocket",
        "operator": "robert",
        "memo": "Sew, trim & bag",
        "due": {
            "year": 2022,
            "month": 12,
            "day": 1,
            "hour": 22,
            "minute": 18
        },
        "frame_info": {
            "offset_h": 10,
            "offset_v": 50,
            "p1_h": 210,
            "p1_v": 4,
            "p2_h": 2600,
            "p2_v": -1600
        },
        "double_byte_characters": false,
        "local_design_name": "AcmeCorporateLogo",
        "image": "Base64 image binary ..."
    },
    "fdr3_palette": {
      "first_stitch_color": "C15",
      "background_color": "#F0FF00",
      "threads": [
        {
          "needle": 1,
          "color": "C01",
          "speed_max": 600,
          "serial": "1801",
          "name": "White",
          "thread_type": "Madeira Polyneon",
          "rgb": "#FEFEFE"
        },
        {
          "needle": -1,
          "color": "C02",
          "speed_max": 600,
          "serial": "1800",
          "name": "Black",
          "thread_type": "Madeira Polyneon",
          "rgb": "#010101"
        },
        {
          "needle": -1,
          "color": "C03",
          "speed_max": 800,
          "serial": "1755",
          "name": "Red",
          "thread_type": "Madeira Polyneon",
          "rgb": "#800000"
        }
      ]
    },
    "prj_info": {
      "v_scale": 100,
      "h_scale": 200,
      "rot_pattern": 1,
      "angle": 0,
      "origin": 1,
      "socks": 1,
      "applique": 0,
      "a_h_offset": 0,
      "a_v_offset": 0,
      "frame_out": 0,
      "f_h_offset": 0,
      "f_v_offset": 0,
      "cap_frame": 0,
      "frame_type": 0,
      "repeat": 1,
      "matrix": 0,
      "v_repeat": 1,
      "h_repeat": 1,
      "v_space": 0,
      "h_space": 0,
      "start_dir": 0,
      "swing_type": 0,
      "frm_offset_h": 0,
      "frm_offset_v": 0,
      "frm_p1_h": 0,
      "frm_p1_v": 0,
      "frm_p2_h": 0,
      "frm_p2_v": 0
    },
    "needles": [
      5,
      4,
      3
    ],
    "design_file": "Base64 design binary ..."
}

```

### Request Body Parameters:

| Name                   | Type    | Description                                                                                                                      |
| :--------------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------- |
| <b>fdr3</b>            | Object  | Optional FDR3 production information to apply to the embroidery file.                                                            |
| product_number         | String  | Production Number.                                                                                                               |
| item_name              | String  | Product Name.                                                                                                                    |
| product_type           | String  | Reserve 1.                                                                                                                       |
| qty                    | Integer | Qty to sew.                                                                                                                      |
| speed_start            | Integer | Start Speed.                                                                                                                     |
| speed_max              | Integer | Max Speed.                                                                                                                       |
| frame_name             | String  | Frame name.                                                                                                                      |
| frame_outline_name     | String  | Frame Filename.                                                                                                                  |
| backing_type           | String  | Backing paper.                                                                                                                   |
| where_to_sew           | String  | Embroidery location on garment.                                                                                                  |
| operator               | String  | <not used>                                                                                                                       |
| memo                   | String  | Production Notes.                                                                                                                |
| due                    | Object  | Due Date.                                                                                                                        |
| frame_info             | Object  | Frame Position name.                                                                                                             |
| double_byte_characters | String  | Use Double byte characters if 1 (true).                                                                                          |
| local_design_name      | String  | Local design name or title.                                                                                                      |
| image                  | String  | Image- base64 encoided PNG or JPG, please restrict to QVGA.                                                                      |
| <b>fdr3_palette</b>    | Object  | Thread Color/information for FDR3.                                                                                               |
| first_stitch_color     | String  | Stating color number.                                                                                                            |
| background_color       | String  | Background color, in format "#F0FF00".                                                                                           |
| threads                | Object  | Object with thread information.                                                                                                  |
| needle                 | Integer | Needle Number. <depracated> set to -1.                                                                                           |
| color                  | String  | Color Function Number. C01-C31.                                                                                                  |
| speed_max              | Integer | Max speed for this thread.                                                                                                       |
| serial                 | String  | Thread ID (serial number). Required.                                                                                             |
| name                   | String  | Name of thread. Required.                                                                                                        |
| thread_type            | String  | Chart of thread.                                                                                                                 |
| rgb                    | String  | Thread Color, RGB, in form "#F0FF00".                                                                                            |
| <b>prj_info</b>        | Object  | PRJ informaiton to apply to the embroidery file.                                                                                 |
| v_scale                | Integer | V axis scaling, used for special hoops/clamps.                                                                                   |
| h_scale                | Integer | H axis scaling, used for special hoops/clamps.                                                                                   |
| rot_pattern            | Integer | Rotation Pattern.                                                                                                                |
| angle                  | Integer | Rotation Angle, 0-89 degrees.                                                                                                    |
| origin                 | Integer | Specifies whether to return to Origin.                                                                                           |
| socks                  | Integer | Specifiy SOCKS mode.                                                                                                             |
| applique               | Integer | Enable Applique.                                                                                                                 |
| a_h_offset             | Integer | Applique H movement amount.                                                                                                      |
| a_v_offset             | Integer | Applique V movement amount.                                                                                                      |
| frame_out              | Integer | Enable Frame Exchange.                                                                                                           |
| f_h_offset             | Integer | Frame exchange H movement amount.                                                                                                |
| f_v_offset             | Integer | Frame exchange V movement amount.                                                                                                |
| cap_frame              | Integer | Specifies Cap Frame Type.                                                                                                        |
| frame_type             | Integer | The frame type.                                                                                                                  |
| repeat                 | Integer | The number of repetitions.                                                                                                       |
| matrix                 | Integer | MATRIX Settings.                                                                                                                 |
| v_repeat               | Integer | Number of "V" rows.                                                                                                              |
| h_repeat               | Integer | Number of "H" columns.                                                                                                           |
| v_space                | Integer | Space between V's.                                                                                                               |
| h_space                | Integer | Space betweeh H's.                                                                                                               |
| start_dir              | Integer | Matrix starting direction.                                                                                                       |
| swing_type             | Integer | Direction of Swing machine paramater movement.                                                                                   |
| frm_offset_h           | Integer | Frame position H movement amount.                                                                                                |
| frm_offset_v           | Integer | Frame position V movement amount.                                                                                                |
| frm_p1_h               | Integer | The H position of frame position P1.                                                                                             |
| frm_p1_v               | Integer | The V position of frame position P1.                                                                                             |
| frm_p2_h               | Integer | The H position of frame position P2.                                                                                             |
| frm_p2_v               | Integer | The V position of frame position P2.                                                                                             |
| <b>needles</b>         | Array   | List of needles to assign, for converting a DST to a U01/U53 file.                                                               |
| <b>design_file</b>     | String  | Stitch data to upload, string value in Base64.                                                                                   |


### Response:

```json
{
    "file_name": [
        "123456789"
    ]
}
```

### Fields:

| Name      | Type  | Description                         |
| :-------- | :---- | :---------------------------------- |
| file_name | Array | Returns the name of the saved file. |


### Errors:

| Code | Description                       |
| :--- | :-------------------------------- |
| 404  | The resource cannot be found.     |
| 500  | An error has occurred internally. |

{% endapi %}
