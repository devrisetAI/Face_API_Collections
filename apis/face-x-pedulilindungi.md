---
description: >-
  This section contains the API that integrates with PeduliLindungi for face
  recognition.
---

# Face X PeduliLindungi API

![](../.gitbook/assets/screenshot-2021-09-06-at-16-24-48-face-verification-x-pedulilindungi-api-client-docs-hackmd.png)

## **POST `/pedulilindungi/enroll-face`**

This API registers a user to the database.

### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "nik":              "3273022807762",
  "user_name":        "RisetAi Username1",
  "facegallery_id":   "riset.ai@production",
  "image":            "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
  "trx_id":           "alphanumericalstring1234"
}
```

| Key              | Type     | Description                                                                      |
| ---------------- | -------- | -------------------------------------------------------------------------------- |
| `nik`            | `string` | NIK number in KTP (must be exactly the same)                                     |
| `user_name`      | `string` | Name in KTP (must be exactly the same)                                           |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc) |
| `image`          | `string` | Base64 encoded JPG or PNG image                                                  |
| `trx_id`         | `string` | Unique transaction identifier, for transaction logging and debugging purposes    |

### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
  "status":           "200",
  "status_message":   "Success",
  "pl_data": {
        "success": true,
        "code": 200,
        "message": "Login checkout Success",
        "apiVersion": "v1"
    }
}
```

| Key              | Type     | Description                                                                                                                                                                                     |
| ---------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `status`         | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)                                                                                    |
| `status_message` | `string` | The verbose message of API hit status, please refer to[ List of Status Code](../others/list-of-status-code.md)                                                                                  |
| `pl_data`        | `list`   | PeduliLindungi API response for registration, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |

## **POST `/pedulilindungi/list-faces`**

This API gives a list of the registered user.

### **Request**

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

### **Response**

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
          "nik":      "3273022807762",
          "user_name":"RisetAi Username1"
      },
      {
          "nik":      "32730228077623", 
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

## **POST `/pedulilindungi/verify-checkin-checkout`**

This API verifies an image with a registered user.

### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "qr_code":          "checkin:60dd9e2bac68e40011056662",
  "latitude":         -8.068494,
  "longitude":        111.8992385,
  "nik":              "3273022807762",
  "facegallery_id":   "riset.ai@production",
  "image":            "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
  "trx_id":           "alphanumericalstring1234",
  "minimum_confidence_level":0.95
}
```

| Key                        | Type      | Description                                                                                                                                                             |
| -------------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `qr_code`                  | `string`  | Value scanned QRCode, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |
| `latitude`                 | `float`   | Latitude of QRCode, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf)   |
| `longitude`                | `float`   | Longitude of QRCode, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf)  |
| `nik`                      | `string`  | NIK number in KTP (must be exactly the same)                                                                                                                            |
| `facegallery_id`           | `string`  | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc)                                                                                        |
| `image`                    | `string`  | Base64 encoded JPG or PNG image                                                                                                                                         |
| `trx_id`                   | `string`  | Unique transaction identifier, for transaction logging and debugging purposes                                                                                           |
| `minimum_confidence_level` | `float64` | Requested minimum confidence\_lv threshold, for requesting PL API, **this is optional**                                                                                 |

### **Response**

#### **`Headers`**

| KEY              | VALUE              |
| ---------------- | ------------------ |
| **Content-Type** | `application/json` |

#### **`Body`**

```javascript
{
 "status":        "200",
 "status_message":"Success",
 "similarity":    1,
 "masker":        false,
 "verified":      true,
 "user_status":   "green",
 "pl_data":       { 
                   ...
                  }
}
```

## **POST `/pedulilindungi/identify-checkin-checkout`**

This API identifies an image with a registered user.

### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "qr_code":          "checkin:60dd9e2bac68e40011056662",
  "latitude":         -8.068494,
  "longitude":        111.8992385,
  "facegallery_id":   "riset.ai@production",
  "image":            "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
  "trx_id":           "alphanumericalstring1234",
  "minimum_confidence_level":0.95
}
```

| Key                        | Type      | Description                                                                                                                                                             |
| -------------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `qr_code`                  | `string`  | Value scanned QRCode, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |
| `latitude`                 | `float`   | Latitude of QRCode, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf)   |
| `longitude`                | `float`   | Longitude of QRCode, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf)  |
| `facegallery_id`           | `string`  | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc)                                                                                        |
| `image`                    | `string`  | Base64 encoded JPG or PNG image                                                                                                                                         |
| `trx_id`                   | `string`  | Unique transaction identifier, for transaction logging and debugging purposes                                                                                           |
| `minimum_confidence_level` | `float64` | Requested minimum confidence\_lv threshold, for requesting PL API, **this is optional**                                                                                 |

### **Response**

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
  ],
 "pl_data":    { 
               ...
               }
}
```

| Key                | Type      | Description                                                                                                                                                                                           |
| ------------------ | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `status`           | `string`  | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md)                                                                                          |
| `status_message`   | `string`  | The verbose message of API hit status, please refer to [List Status Code](../others/list-of-status-code.md)                                                                                           |
| `confidence_level` | `float`   | Describe confidence of model, scale 0.0 to 1.0 (from 0% to 100% confidence)                                                                                                                           |
| `mask`             | `boolean` | If a person’s face wearing a mask, will return True, else return False                                                                                                                                |
| `user_id`          | `string`  | Unique user identifier, alphanumeric (eg. #NIK)                                                                                                                                                       |
| `user_name`        | `string`  | The name of the person who has the `user_id`                                                                                                                                                          |
| `pl_data`          | `string`  | PeduliLindungi API response for check-in check-out, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |

## **DELETE `/pedulilindungi/delete-face`**

This API deletes a user.

### **Request**

#### **`Headers`**

| KEY             | VALUE               |
| --------------- | ------------------- |
| **Accesstoken** | `oauth Accesstoken` |

#### **`Body`**

```javascript
{
  "nik":            "3273022807762",
  "facegallery_id": "riset.ai@production",
  "trx_id":         "alphanumericalstring1234"
}
```

| Key              | Type     | Description                                                                      |
| ---------------- | -------- | -------------------------------------------------------------------------------- |
| `user_id`        | `string` | NIK number in KTP (must be exactly the same)                                     |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric (eg. LocationName, CompanyName, etc) |
| `trx_id`         | `string` | Unique transaction identifier, for transaction logging and debugging purposes    |

### **Response**

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
