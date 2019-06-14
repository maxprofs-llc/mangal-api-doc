---
weight: 20
title: Errors
---

# Status code

The mangal API uses the following error codes

| Code  | Meaning                                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| 200       | Successfull response from the API (`GET`, `PUT`, `DELETE`).                                                                          |
| 201    | The request has been fulfilled, resulting in the creation of a new resource (`POST`).                                                |
| 400  | Bad Request, API failed to validate the body content.                                                                                |
| 404 | Not Found, endpoint doesn't exist.                                                                                                   |
| 500  | Internal Server Error, problem with our server. Try again later or email the system administrator - steve.vissault[at]usherbrooke.ca |
| 503 | Service Unavailable -- We're temporarily offline for maintenance.                                                                    |
