---
description: This page contains all of the status codes are used on this API.
---

# List of Status Code

```text
200 : Success meassages

400 : General Request Malformed
401 : Not Accesstoken Not Authorized
403 : General Requested Resource Denied

411 : Business Process Warning - Face Not Verified or Unregistered
412 : Procedural Error - Face not detected
413 : Procedural Error - Face too small
414 : Procedural Error - Multiple face found

415 : Resource Not Found - UserID Not Found
416 : Resource Not Found - FaceGallery Not Found

451 : Data Format Error - image is null
452 : Data Format Error - user_id is null
453 : Data Format Error - user_name is null
454 : Data Format Error - facegallery_id is null
455 : Data Format Error - target_image is null
456 : Data Format Error - source_image is null

490 : Image Error - cannot decode image base64
491 : Image Error - image type not recognized
492 : Image Error - cannot decode target_image base64
493 : Image Error - target_image type not recognized
494 : Image Error - cannot decode source_image base64
495 : Image Error - source_image type not recognized

500 : Procedural Error - Server Error
```

