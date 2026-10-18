# API Test Plan

These test cases define the acceptance criteria for the REST API contract. They ensure both valid actions (positive paths) and invalid actions (negative paths) handle responses correctly.

| Test ID | Request                                                    | Expected Result                                                    | Actual Result                                        | Pass/Fail |
| :------ | :--------------------------------------------------------- | :----------------------------------------------------------------- | :--------------------------------------------------- | :-------- |
| **T01** | GET `/api/issues`                                          | `200`; full JSON array of stored issues.                           | `200`; array returned                                | Pass      |
| **T02** | POST valid `title`, `description`, `priority`              | `201`; complete issue with server-generated fields.                | Not run                                              | Pending   |
| **T02** | POST valid `title`, `description`, `priority`              | `201`; complete issue with server-generated fields.                | `201`; generated id, `Open` status and ISO timestamp | Pass      |
| **T03** | POST missing required `title` field                        | `400`; `VALIDATION_ERROR` payload.                                 | Not run                                              | Pending   |
| **T03** | POST missing required `title` field                        | `400`; `VALIDATION_ERROR` payload.                                 | `400`; title length validation message               | Pass      |
| **T04** | POST invalid priority value (e.g., `Critical`)             | `400`; `VALIDATION_ERROR` payload.                                 | Not run                                              | Pending   |
| **T04** | POST invalid priority value (e.g., `Critical`)             | `400`; `VALIDATION_ERROR` payload.                                 | `400`; priority validation message                   | Pass      |
| **T05** | PATCH existing issue status to `Resolved`                  | `200`; updated issue shows `status: "Resolved"`.                   | Not run                                              | Pending   |
| **T05** | PATCH existing issue status to `Resolved`                  | `200`; updated issue shows `status: "Resolved"`.                   | `200`; issue status is `Resolved`                    | Pass      |
| **T06** | PATCH issue status with an invalid value (e.g., `Deleted`) | `400`; `VALIDATION_ERROR` payload.                                 | Not run                                              | Pending   |
| **T06** | PATCH issue status with an invalid value (e.g., `Deleted`) | `400`; `VALIDATION_ERROR` payload.                                 | `400`; status validation message                     | Pass      |
| **T07** | PATCH status for an unknown issue ID                       | `404`; `ISSUE_NOT_FOUND` error payload.                            | Not run                                              | Pending   |
| **T07** | PATCH status for an unknown issue ID                       | `404`; `ISSUE_NOT_FOUND` error payload.                            | `404`; `ISSUE_NOT_FOUND`                             | Pass      |
| **T08** | GET `/api/issues` when no issues exist                     | `200`; clean, empty JSON array `[]`.                               | Not run                                              | Pending   |
| **T08** | GET `/api/issues` when no issues exist                     | `200`; clean, empty JSON array `[]`.                               | `200`; empty array                                   | Pass      |
| **T09** | POST with extra server-owned fields                        | `201`; client-provided `id`, `status` and `createdAt` are ignored. | Not run                                              | Pending   |
| **T09** | POST with extra server-owned fields                        | `201`; client-provided `id`, `status` and `createdAt` are ignored. | `201`; server-generated values retained              | Pass      |
| **T10** | POST `/api/issues` without JSON content type               | `415`; `UNSUPPORTED_MEDIA_TYPE` payload.                           | Not run                                              | Pending   |
| **T10** | POST `/api/issues` without JSON content type               | `415`; `UNSUPPORTED_MEDIA_TYPE` payload.                           | `415`; `UNSUPPORTED_MEDIA_TYPE`                      | Pass      |
| **T11** | POST `/api/issues` with malformed JSON                     | `400`; `VALIDATION_ERROR` payload and server remains running.      | Not run                                              | Pending   |
| **T11** | POST `/api/issues` with malformed JSON                     | `400`; `VALIDATION_ERROR` payload and server remains running.      | `400`; malformed JSON message; server remained up    | Pass      |
| **T12** | Request an unknown method/path, e.g. `PATCH /api/fake-url` | `404`; `ROUTE_NOT_FOUND` payload.                                  | Not run                                              | Pending   |
| **T12** | Request an unknown method/path, e.g. `PATCH /api/fake-url` | `404`; `ROUTE_NOT_FOUND` payload.                                  | `404`; `ROUTE_NOT_FOUND`                             | Pass      |
