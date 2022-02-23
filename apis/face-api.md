---
description: This section contains the API used to face verification and recognition.
---

# Face API

## **Client Endpoints**

### **POST `/client/register`**

This API registers a client to the database.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

* `None`

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
    "status":           "200",
    "status_message":   "Success",
    "facegallery_id":   "riset.ai@trial"
}
```

| Key              | Type     | Description                                                                                                    |
| ---------------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `status`         | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)   |
| `status_message` | `string` | The verbose message of API hit status, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `facegallery_id` | `string` | Name of facegallery                                                                                            |

### **POST `/client/delete`**

This API deletes the client from the database.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

* `None`

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
    "status":           "200",
    "status_message":   "Success",
    "facegallery_id":   [
        "riset.ai@trial",
        "riset.ai@production"
    ]
}
```

| Key              | Type     | Description                                                                                                    |
| ---------------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `status`         | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)   |
| `status_message` | `string` | The verbose message of API hit status, please refer to[ List of Status Code](../others/list-of-status-code.md) |
| `face_galleryid` | `list`   | List of remaining facegallery                                                                                  |

### **GET `/client/get-counters`**

This API fetches client's API Counters Remaining Quota (API Hits, Num Faces Enrolled, & Num FaceGallery Owned).

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```
{
    "trx_id" : "alphanumericalstring1234"
}
```

| Key      | Type     | Description                                                                   |
| -------- | -------- | ----------------------------------------------------------------------------- |
| `trx_id` | `string` | Unique transaction identifier, for transaction logging and debugging purposes |

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```
{
    "status": "200",
    "status_message": "Success",
    "remaining_limit": {
        "n_api_hits": 9743,
        "n_face": 346,
        "n_facegallery": 3
    }
}
```

| Key               | Type     | Description                                                                                                    |
| ----------------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `status`          | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)   |
| `status_message`  | `string` | The verbose message of API hit status, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `remaining_limit` | `array`  | Contains counters remaining quota/limit                                                                        |
| `n_api_hits`      | `int`    | API Hits remaining limit                                                                                       |
| `n_face`          | `int`    | Remaining number of faces elligible to enroll                                                                  |
| `n_facegallery`   | `int`    | Remaining number of facegallery elligible to create                                                            |

## **Facegallery Endpoints**

### **GET `/facegallery/my-facegalleries`**

This API gives the list of facegallery.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

* `None`

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":           "200",
  "status_message":   "Success - FaceGalleries Listed",
  "facegallery_id": [
      "riset.ai@trial",
      "riset.ai@production"
  ]
}
```

| Key              | Type     | Description                                                                                                    |
| ---------------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `status`         | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)   |
| `status_message` | `string` | The verbose message of API hit status, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `facegallery_id` | `list`   | List of facegallery                                                                                            |

### **POST `/facegallery/create-facegallery`**

This API creates the new face gallery.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "facegallery_id":   "riset.ai@production",
  "trx_id":           "alphanumericalstring1234"
}
```

| Key              | Type     | Description                                                                   |
| ---------------- | -------- | ----------------------------------------------------------------------------- |
| `facegallery_id` | `string` | Name of facegallery                                                           |
| `trx_id`         | `string` | Unique transaction identifier, for transaction logging and debugging purposes |

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":           "200",
  "status_message":   "Success",
  "facegallery_id":   "riset.ai@production"
}
```

| Key              | Type     | Description                                                                                                    |
| ---------------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `status`         | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)   |
| `status_message` | `string` | The verbose message of API hit status, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `facegallery_id` | `string` | Name of facegallery                                                                                            |

### **DELETE `/facegallery/delete-facegallery`**

This API deletes a facegallery.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "facegallery_id": "riset.ai@production",
  "trx_id":         "alphanumericalstring1234"
}
```

| Key              | Type     | Description                                                                   |
| ---------------- | -------- | ----------------------------------------------------------------------------- |
| `facegallery_id` | `string` | Name of facegallery                                                           |
| `trx_id`         | `string` | Unique transaction identifier, for transaction logging and debugging purposes |

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":           "200",
  "status_message":   "Success",
  "facegallery_id":   "riset.ai@production"
}
```

| Key              | Type     | Description                                                                                                    |
| ---------------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `status`         | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)   |
| `status_message` | `string` | The verbose message of API hit status, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `facegallery_id` | `string` | Name of deleted facegallery                                                                                    |

## **User Endpoints**

### **POST `/facegallery/enroll-face`**

This API registers a user to the database.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "user_id":          "risetai1234",
  "user_name":        "RisetAi Username1",
  "facegallery_id":   "riset.ai@production",
  "image":            "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
  "trx_id":           "alphanumericalstring1234"
}
```

| Key              | Type     | Description                                                                      |
| ---------------- | -------- | -------------------------------------------------------------------------------- |
| `user_id`        | `string` | Unique user identifier, alphanumeric (eg. #NIK)                                  |
| `user_name`      | `string` | The name of the person who has the `user_id`                                     |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc) |
| `image`          | `string` | Base64 encoded JPG or PNG image                                                  |
| `trx_id`         | `string` | Unique transaction identifier, for transaction logging and debugging purposes    |

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":           "200",
  "status_message":   "Success"
}
```

| Key              | Type     | Description                                                                                                    |
| ---------------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `status`         | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)   |
| `status_message` | `string` | The verbose message of API hit status, please refer to[ List of Status Code](../others/list-of-status-code.md) |

### **GET `/facegallery/list-faces`**

This API gives a list of the registered user.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "facegallery_id": "riset.ai@production",
  "trx_id":         "alphanumericalstring1234"
}
```

| Key              | Type     | Description                                                                      |
| ---------------- | -------- | -------------------------------------------------------------------------------- |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc) |
| `trx_id`         | `string` | Unique transaction identifier, for transaction logging and debugging purposes    |

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":           "200",
  "status_message":   "Success",
  "faces": [
      {
          "user_id":  "risetai1234",
          "user_name":"RisetAi Username1"
      },
      {
          "user_id":  "risetai5678",
          "user_name":"RisetAi Username2"
      }
  ]
}
```

| Key              | Type     | Description                                                                                                    |
| ---------------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `status`         | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)   |
| `status_message` | `string` | The verbose message of API hit status, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `faces`          | `list`   | List of registered user                                                                                        |

### **POST `/facegallery/verify-face`**

This API verifies an user\_id and an image with a registered user or it does 1:1 authentication.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "user_id":          "risetai1234",
  "facegallery_id":   "riset.ai@production",
  "image":            "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
  "trx_id":           "alphanumericalstring1234"
}
```

| Key              | Type     | Description                                                                      |
| ---------------- | -------- | -------------------------------------------------------------------------------- |
| `user_id`        | `string` | Unique user identifier, alphanumeric (eg. #NIK)                                  |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc) |
| `image`          | `string` | Base64 encoded JPG or PNG image                                                  |
| `trx_id`         | `string` | Unique transaction identifier, for transaction logging and debugging purposes    |

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":           "200",
  "status_message":   "Success",
  "user_name":        "RisetAi Username",
  "similarity":       1,
  "masker":           false,
  "verified":         true,
}
```

| Key              | Type      | Description                                                                                                  |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------ |
| `status`         | `string`  | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `status_message` | `string`  | The verbose message of API hit status, please refer to [List Status Code](../others/list-of-status-code.md)  |
| `user_name`      | `string`  | Username                                                                                                     |
| `similarity`     | `float`   | Describe the comparison of facial similarities, scale 0.0 to 1.0 (from 0% to 100% similar)                   |
| `masker`         | `boolean` | If a person’s face wearing a mask, will return True, else return False                                       |
| `verified`       | `boolean` | If similarity above set config parameter(eg. threshold = 0.75), return True, else return False               |

### **POST `/facegallery/identify-face`**

This API identify an image with a registered user or it do 1:N authentication.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "facegallery_id":   "riset.ai@production",
  "image":            "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
  "trx_id":           "alphanumericalstring1234"
}
```

| Key              | Type     | Description                                                                      |
| ---------------- | -------- | -------------------------------------------------------------------------------- |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc) |
| `image`          | `string` | Base64 encoded JPG or PNG image                                                  |
| `trx_id`         | `string` | Unique transaction identifier, for transaction logging and debugging purposes    |

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":               "200",
  "status_message":       "Success",
  "status_description":   "Face Recognition Success",
  "return": [
      {
          "confidence_level": "0.943697",
          "mask":             "true",
          "user_id":          "risetai1234",
          "user_name":        "RisetAi Username1"
      }
  ]
}
```

| Key                | Type      | Description                                                                                                  |
| ------------------ | --------- | ------------------------------------------------------------------------------------------------------------ |
| `status`           | `string`  | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `status_message`   | `string`  | The verbose message of API hit status, please refer to [List Status Code](../others/list-of-status-code.md)  |
| `confidence_level` | `float`   | Describe confidence of model, scale 0.0 to 1.0 (from 0% to 100% confidence)                                  |
| `mask`             | `boolean` | If a person’s face wearing a mask, will return True, else return False                                       |
| `user_id`          | `string`  | Unique user identifier, alphanumeric (eg. #NIK)                                                              |
| `user_name`        | `string`  | The name of the person who has the `user_id`                                                                 |

### **DELETE `/facegallery/delete-face`**

This API deletes a user.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "user_id":        "risetai1234",
  "facegallery_id": "riset.ai@production",
  "trx_id":         "alphanumericalstring1234"
}
```

| Key              | Type     | Description                                                                      |
| ---------------- | -------- | -------------------------------------------------------------------------------- |
| `user_id`        | `string` | Unique user identifier, alphanumeric (eg. #NIK)                                  |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc) |
| `trx_id`         | `string` | Unique transaction identifier, for transaction logging and debugging purposes    |

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":         "200",
  "status_message": "Success"
}
```

| Key              | Type     | Description                                                                                                    |
| ---------------- | -------- | -------------------------------------------------------------------------------------------------------------- |
| `status`         | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)   |
| `status_message` | `string` | The verbose message of API hit status, please refer to [List of Status Code](../others/list-of-status-code.md) |

### **POST `/compare-images`**

This API compares the two images to determine if they are verified or not. This API does not use the information in the database.

#### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "source_image": "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
  "target_image": "/9j/4AAQSkZJRgABAQEASABIAAD/389sdAxcZisA...",
  "trx_id":       "alphanumericalstring1234"
}
```

| Key            | Type     | Description                                                                   |
| -------------- | -------- | ----------------------------------------------------------------------------- |
| `source_image` | `string` | Base64 encoded JPG or PNG of compared image                                   |
| `target_image` | `string` | Base64 encoded JPG or PNG of the reference image                              |
| `trx_id`       | `string` | Unique transaction identifier, for transaction logging and debugging purposes |

#### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":         "200",
  "status_message": "Success",
  "similarity":     0.8308,
  "verified":       true,
  "masker":         true
}
```

| Key              | Type      | Description                                                                                                  |
| ---------------- | --------- | ------------------------------------------------------------------------------------------------------------ |
| `status`         | `string`  | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `status_message` | `string`  | The verbose message of API hit status, please refer to [List Status Code](../others/list-of-status-code.md)  |
| `similarity`     | `float`   | Describe the comparison of facial similarities, scale 0.0 to 1.0 (from 0% to 100% similar)                   |
| `verified`       | `boolean` | If similarity above set config parameter(eg. threshold = 0.75), return True, else return False               |
| `masker`         | `boolean` | If a person’s face wearing a mask, will return True, else return False                                       |
