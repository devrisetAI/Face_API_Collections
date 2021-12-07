---
description: This section contains documentation on Liveness API usage and functions
---

# Liveness API
![](../.gitbook/assets/risetai\_logo.72c56424.png)

## **POST `/liveness-api/verify-face-liveness`**

This API predicts liveness of face from two type active and passive. Given a requested `parameter`, will return `True` or `False` depending on the API's prediction

### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```json
{  
    "facegallery_id"    : "riset.ai@production",
    "user_id"           : "risetai1234",
    "trx_id"            : "alphanumericalstring1234",
    "spoof_detection"   : true,
    "success_threshold" : 8,
    "face_parameters"   : [
        "left",
        "right",
        "up",
        "front",
        "eyes open",
        "eyes closed",
        "mouth open",
        "mouth closed"
    ],
    "images"            :[
        "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
        "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
        "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
        "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
        "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
        "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
        "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
        "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
    ]
}
```

| Key | Type | Description | Optional |
| - | - | - | - |
| `user_id`               | `string` | Unique User/Face Identifier, **optional but recommended** (paired with `facegallery_id`) | &#9745; |
| `facegallery_id`        | `string` | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc), **optional but recommended** (paired with `user_id`) | &#9745; |
| `spoof_detection`                | `bool` | Specify whether to do spoof detection or not, will default to `true` if none specified, **optional** | &#9745; |
| `success_threshold`                | `int` | Minimal number of successful image liveness detection, will default to all images if none specified, **optional** | &#9745; |
| `trx_id`                | `string` | Unique transaction identifier, for transaction logging and debugging | &#9744; |
| `images`                | `list of string` | List of Base64 encoded JPG or PNG image, **number of `images` must be the same as `face_parameters`** | &#9744;  |
| `face_parameters`       | `list of string`  | contains requested parameters to match with API prediction, see `"*"` below for possible parameters, **number of `face_parameters` must be the same as `images`** | &#9744; |

`* face_parameters:`
```
    "left",
    "right",
    "up",
    "down",
    "front",
    "eyes open",
    "eyes closed",
    "mouth open",
    "mouth closed"
```
### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```json
{
    "status": "200",
    "status_message": "Success",
    "liveness": "passed",
    "results": {
        "image1": {
            "match": true,
            "verified": true,
            "similarity": 0.96,
            "masker": true,
            "spoof": "spoof",
            "spoof_score": 0.7680,
            "roll": -0.4,
            "pitch": 19.32,
            "yaw": 6.13,
            "left_eye": "open",
            "left_eye_score": 0.9999,
            "right_eye": "open",
            "right_eye_score": 1.0,
            "mouth": "closed",
            "mouth_score": 0.9762
        },
        "image2": {
            "match": true,
            "verified": true,
            "similarity": 0.96,
            "masker": false,
            "spoof": "spoof",
            "spoof_score": 0.7680,
            "roll": -2.18,
            "pitch": 8.27,
            "yaw": -1.01,
            "left_eye": "open",
            "left_eye_score": 0.9999,
            "right_eye": "open",
            "right_eye_score": 1.0,
            "mouth": "closed",
            "mouth_score": 0.9762
        },
        ...
        "image_n_: {
            ...,
        }
    }
}
```

| Key                  | Type      | Description                                                                                                                         |
| -------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `status`             | `string`  | Describing the condition of API hit |
| `status_message`     | `string`  | The verbose message of API hit status |
| `liveness`   | `string`   | Describes if the requested images are considered `"alive"` |
| `results`| `array` | Contains detailed info for each requested images |
| `results.image_n`| `array` | Contains detailed info of processed image, will be dynamic depending on requested parameter |
| `results.image_n.match`| `bool` | If image matches the requested parameter, will return `True` |
| `results.image_n.verified`| `bool` | If face considered verified, will return `True` |
| `results.image_n.similarity`| `float` | Face similarity score |
| `results.image_n.masker`| `bool` | If face wears masker, will return `True` |
| `results.image_n.spoof`| `string` | If image is considered spoof, will return `spoof`, else, `real` |
| `results.image_n.spoof_score`| `float` | Spoof detection score |
| `results.image_n.roll`| `float` | Predicted face roll degree |
| `results.image_n.pitch`| `float` | Predicted face pitch degree |
| `results.image_n.yaw`| `float` | Predicted face yaw degree |
| `results.image_n.left_eye`| `string` | If image contains opened left eye, will return `open`, else, `closed` |
| `results.image_n.left_eye_score`| `float` | Predicted left_eye score |
| `results.image_n.right_eye`| `bool` | If image contains opened right eye, will return `open`, else, `closed` |
| `results.image_n.right_eye_score`| `float` | Predicted right_eye score |
| `results.image_n.mouth`| `bool` | If image contains opened mouth, will return `open`, else, `closed` |
| `results.image_n.mouth_score`| `float` | Predicted mouth score |
