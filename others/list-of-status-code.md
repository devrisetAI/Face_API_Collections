---
description: This page contains all of the status codes are used on this API.
---

# List of Status Code

| Status Code | Type                     | Desctiption                         |
| ----------- | ------------------------ | ----------------------------------- |
| 200         | Succes                   | Success messages                    |
| 400         | General Error            | Request malformed                   |
| 401         | General Error            | Accestoken not authorized           |
| 403         | General Error            | Requested resource denied           |
| 411         | Business Process Warning | Face not verified or unregistered   |
| 412         | Business Process Warning | Face not detected                   |
| 413         | Business Process Warning | Face too small                      |
| 415         | Resource Not Found       | `user_id` not found                 |
| 416         | Resource Not Found       | `facegallery_id` not found          |
| 451         | Resource Not Found       | `image` is null                     |
| 452         | Data Format Error        | `user_id` is null                   |
| 453         | Data Format Error        | `user_name` is null                 |
| 454         | Data Format Error        | `facegallery_id` is null            |
| 455         | Data Format Error        | `target_image` is null              |
| 456         | Data Format Error        | `source_image` is null              |
| 490         | Image Error              | Cannot decode `image` base64        |
| 491         | Image Error              | `image` type not recognized         |
| 492         | Image Error              | Cannot decode `target_image` base64 |
| 493         | Image Error              | `image` error                       |
| 494         | Image Error              | Cannot decode `source_image` base64 |
| 495         | Image Error              | `source_image` type not recognized  |
| 500         | Procedula Error          | Server error                        |
