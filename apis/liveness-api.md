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

```javascript
{      
    "facegallery_id": "riset.ai@production",
    "user_id":        "risetai1234",
    "image":          "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
    "trx_id":         "alphanumericalstring1234",
    "face_parameters" : {
        "angle":    "left",
        "spoof":    "strict",
        "eyes":     "closed",
        "mouth":    "open"
    }
}
```

| Key                     | Type     | Description                                                                                                                                                               |
| ----------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `user_id`               | `string` | Unique User/Face Identifier, **this is optional** (paired with `facegallery_id`)                                                                                          |
| `facegallery_id`        | `string` | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc), **this** **is optional** (paired with `user_id`)                                        |
| `image`                 | `string` | Base64 encoded JPG or PNG image                                                                                                                                           |
| `trx_id`                | `string` | Unique transaction identifier, for transaction logging and debugging purposes                                                                                             |
| `face_parameters`       | `array`  | contains requested parameters to match with API prediction, at least `one` `parameter` is needed                                                                          |
| `face_parameters.angle` | `string` | "left" or "right", API will predict if the input `image` is the facing `left` or `right`, **this is optional**                                                            |
| `face_parameters.spoof` | `string` | "strict" or "loose", API will predict if the input `image` contains REAL face or not. `strict` for stricter threshold, and `loose` for the opposite, **this is optional** |
| `face_parameters.eyes`  | `string` | "open" or "closed", API will predict if the input `image` contains a face with `open` or `closed` eyes, **this is optional**                                              |
| `face_parameters.mouth` | `string` | "open" or "closed", API will predict if the input `image` contains a face with `open` or `closed` mouth, **this is optional**                                             |

### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
    "status": "200",
    "status_message": "Success",
    "confidence_level": 0.7348,
    "verified": false,
    "match_status": {
        "spoof": true,
        "angle": false,
        "eyes": false,
        "mouth": true
    },
    "face_attributes": {
        "spoof": "real",
        "roll": -2.32,
        "pitch": -8.82,
        "yaw": 25.01,
        "left_eye": "open",
        "right_eye": "open",
        "mouth": "closed"
    }
}
```

| Key                  | Type      | Description                                                                                                                         |
| -------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `status`             | `string`  | Describing the condition of API hit                                                                                                 |
| `status_message`     | `string`  | The verbose message of API hit status                                                                                               |
| `confidence_level`   | `float`   | Describe confidence of model, scale 0.0 to 1.0 (from 0% to 100% confidence)                                                         |
| `verified`           | `boolean` | If confidence\_level above threshold, returns `True`                                                                                |
| `match_status`       | `array`   | Contains result of requested `face_parameters`                                                                                      |
| `match_status.angle` | `boolean` | Returns `True` if API predicts the same result as requested `face_parameters.angle`, will only return if requested                  |
| `match_status.spoof` | `boolean` | Returns `True` if score above threshold `strict` or `loose`, as requested in `face_parameters.spoof`, will only return if requested |
| `match_status.eyes`  | `boolean` | Returns `True` if API predicts the same result as requested `face_parameters.eyes`, will only return if requested                   |
| `match_status.mouth` | `boolean` | Returns `True` if API predicts the same result as requested `face_parameters.mouth`, will only return if requested                  |
| `face_attributes`    | `array`   | Contains a more detailed result of predicted face attributes                                                                        |
