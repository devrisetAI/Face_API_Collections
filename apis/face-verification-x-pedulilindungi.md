---
description: >-
  This section contains the API that integrates with PeduliLindungi for face
  verification.
---

# Face Verification X PeduliLindungi API

![](../.gitbook/assets/screenshot-2021-09-06-at-16-24-48-face-verification-x-pedulilindungi-api-client-docs-hackmd.png)

## **POST `/pedulilindungi/enroll-face`**

This API registers an user to the database.

### **Request**

#### Headers

* `Accesstoken`

**Body**

```javascript
{
  "nik":              "3273022807762",
  "user_name":        "RisetAi Username1",
  "facegallery_id":   "riset.ai@production",
  "image":            "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
  "trx_id":           "alphanumericalstring1234"
}
```

| Key | Type | Description |
| :--- | :--- | :--- |
| `nik` | `string` | NIK number in KTP \(must be exactly the same\) |
| `user_name` | `string` | Name in KTP \(must be exactly the same\) |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric \(eg. LocationName, CompanyName, etc\) |
| `image` | `string` | Base64 encoded JPG or PNG image |
| `trx_id` | `string` | Unique transaction identifier, for transaction logging and debugging purposes |

### **Response**

#### Headers

* `Content-Type "application/json"`

**Body**

```javascript
{
  "status":           "200",
  "status_message":   "Success"
  "pl_data": {
        "success": true,
        "code": 200,
        "message": "Login checkout Success",
        "apiVersion": "v1"
    }
}
```

| Key | Type | Description |
| :--- | :--- | :--- |
| `status` | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `status_message` | `string` | The verbose message of API hit status, please refer to[ List of Status Code](../others/list-of-status-code.md) |
| `pl_data` | `list` | PeduliLindungi API response for registration, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |



## **POST `/pedulilindungi/list-faces`**

This API gives a list of the registered user.

### **Request**

#### Headers

* `Accesstoken`

**Body**

```javascript
{
  "facegallery_id": "riset.ai@production",
  "trx_id":         "alphanumericalstring1234"
}
```

| Key | Type | Description |
| :--- | :--- | :--- |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric \(eg. LocationName, CompanyName, etc\) |
| `trx_id` | `string` | Unique transaction identifier, for transaction logging and debugging purposes |

### **Response**

#### Headers

* `Content-Type "application/json"`

**Body**

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

| Key | Type | Description |
| :--- | :--- | :--- |
| `status` | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `status_message` | `string` | The verbose message of API hit status, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `faces` | `list` | List of registered user |

## **POST `/pedulilindungi/verify-checkin-checkout`**

This API verifies an image with a registered user.

### **Request**

#### Headers

* `Accesstoken`

**Body**

```javascript
{
  "qrCode":           "checkin:60dd9e2bac68e40011056662",
  "latitude":         -8.068494,
  "longitude":        111.8992385
  "nik":              "3273022807762",
  "facegallery_id":   "riset.ai@production",
  "image":            "/9j/4AAQSkZJRgABAQEASABIAAD/4QBMRXhpZgAA...",
  "trx_id":           "alphanumericalstring1234",
}
```

| Key | Type | Description |
| :--- | :--- | :--- |
| `qrCode` | `string` | Value scanned QRCode, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |
| `latitude` | `float` | Latitude of QRCode, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |
| `longitude` | `float` | Longitude of QRCode, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |
| `nik` | `string` | NIK number in KTP \(must be exactly the same\) |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric \(eg. LocationName, CompanyName, etc\) |
| `image` | `string` | Base64 encoded JPG or PNG image |
| `trx_id` | `string` | Unique transaction identifier, for transaction logging and debugging purposes |

### **Response**

#### Headers

* `Content-Type "application/json"`

**Body**

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

| Key | Type | Description |
| :--- | :--- | :--- |
| `status` | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `status_message` | `string` | The verbose message of API hit status, please refer to [List Status Code](../others/list-of-status-code.md) |
| `similarity` | `float` | Describe the comparison of facial similarities, scale 0.0 to 1.0 \(from 0% to 100% similar\) |
| `masker` | `boolean` | If a person’s face wearing a mask, will return True, else return False |
| `verified` | `boolean` | If similarity above set config parameter\(eg. threshold = 0.75\), return True, else return False |
| `user_status` | `string` | Status from PeduliLindungi API, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |
| `pl_data` | `string` | PeduliLindungi API response for check-in check-out, please refer to [PeduliLindungi Documentation](https://static.bigbox.co.id/web-files/Check%20In%20dan%20Check%20Out%20QR%20Peduli%20Lindungi.pdf) |

## **DELETE `/pedulilindungi/delete-face`**

This API deletes a user.

### **Request**

#### Headers

* `Accesstoken`

**Body**

```javascript
{
  "nik":            "3273022807762",
  "facegallery_id": "riset.ai@production",
  "trx_id":         "alphanumericalstring1234"
}
```

| Key | Type | Description |
| :--- | :--- | :--- |
| `user_id` | `string` | NIK number in KTP \(must be exactly the same\) |
| `facegallery_id` | `string` | Unique FaceGallery identifier, alphanumeric \(eg. LocationName, CompanyName, etc\) |
| `trx_id` | `string` | Unique transaction identifier, for transaction logging and debugging purposes |

### **Response**

#### Headers

* `Content-Type "application/json"`

**Body**

```javascript
{
  "status":         "200",
  "status_message": "Success"
}
```

| Key | Type | Description |
| :--- | :--- | :--- |
| `status` | `string` | Describing the condition of API hit, please refer to [List of Status Code](../others/list-of-status-code.md) |
| `status_message` | `string` | The verbose message of API hit status, please refer to [List of Status Code](../others/list-of-status-code.md) |

