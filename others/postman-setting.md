---
description: This is a tutorial to hit the API with Postman
---

# Tutorial for Hitting API with Postman

## Steps

1. Get the `Accesstoken`.
2. Choose POST, GET or DELETE method.
3. Fill in the URL according to the API you want to do.
4. Choose Header.
5. Choose Body.
6. Choose raw.
7. Change type to JSON.
8. Fill with request JSON text.
9. Click send.
10. Wait for the response.

####  <a id="Example"></a>

## Example

1.Get `access_token` from [AuthTenant](../authtenant.md#1-post-client-login). Copy the `access_token` value.

![](../.gitbook/assets/access-token.png)

2. Set the method and put the URL. \(e.g **POST**`/pedulilindungi/enroll-face`\) 

![](../.gitbook/assets/pswpold.png)

3. Choose Header, and add the `Accesstoken`. 

![](../.gitbook/assets/lqp5isc.png)

4. Choose Body and select RAW, change type file to JSON. 

![](../.gitbook/assets/xhqzlkg.png)

5. Fill with request JSON text on the body like explained above. 

![](../.gitbook/assets/ahk0je6.png)

6. Click `Send` \(pictures number 2\).

7. Wait for the response. If it is successful, there’s will be output in JSON File.

![](../.gitbook/assets/yvz1d8c.png)

8. The response output depends on which requests are used.

