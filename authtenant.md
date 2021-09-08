---
description: >-
  Version 1.0. 7 September 2021. All users of the Riset.ai API must register
  using the method described in this document.
---

# AuthTenant

## **Base URL**

> [https://riset.luqmanr.xyz/oauth](https://riset.luqmanr.xyz/oauth) \(priority\) [  
> https://api.riset.ai/oauth](https://api.riset.ai/api/oauth)

## **1. POST `/client/login`**

### **Description**

This endpoint is used to perform operations related to accounts in **AuthTenant**. For now, this functionality is limited to **Accesstoken** requests.

Will generate a new **Accesstoken** every time it gets a request, it is recommended to take notes.

### **Request**

#### Headers

* `None`

**Body**

* `x-www-form-urlencoded`

| KEY | VALUE |
| :--- | :--- |
| **client\_id** | `riset.ai` |
| **password** | `#password` |

### **Response**

#### Headers

* `Content-Type "application/json"`

**Body**

```javascript
{
  "access_token": "eyJhbGciOiJSUzI1NiIsIn..."
}
```

## **2. POST `/token/revoke`**

### **Description**

This endpoint is used to revoke the previously generated **Accesstoken**. **Accesstoken** will be added to the Blacklist list.

Used if **Accesstoken** leaked to other party, and want to revoke the authorization

### **Request**

#### Headers

| KEY | VALUE |
| :--- | :--- |
| **Accesstoken** | `access token` |

#### Body

* `x-www-form-urlencoded`

| KEY | VALUE |
| :--- | :--- |
| **client\_id** | `riset.ai` |
| **password** | `#hashed-password` |

### **Response**

#### Headers

* `Content-Type "application/json"`

**Body**

```javascript
{
  "status_message": "Success Revoke Token"
}
```

