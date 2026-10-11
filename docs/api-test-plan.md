# API Test Plan

These test cases define the acceptance criteria for the REST API contract. They ensure both valid actions (positive paths) and invalid actions (negative paths) handle responses correctly.

| Test ID | Request Description                                                 | Expected HTTP Status | Expected JSON Output Shape / Result                                                                         |
| :------ | :------------------------------------------------------------------ | :------------------- | :---------------------------------------------------------------------------------------------------------- |
| **T01** | GET `/api/issues`                                                   | `200 OK`             | Full JSON array of all stored issues.                                                                       |
| **T02** | POST valid `title`, `description`, `priority`                       | `201 Created`        | Complete newly created issue object (including server-generated fields).                                    |
| **T03** | POST missing required `title` field                                 | `400 Bad Request`    | `VALIDATION_ERROR` payload.                                                                                 |
| **T04** | POST invalid priority value (e.g., `priority = Critical`)           | `400 Bad Request`    | `VALIDATION_ERROR` payload.                                                                                 |
| **T05** | PATCH existing issue status to `Resolved`                           | `200 OK`             | Updated issue object showing `status: "Resolved"`.                                                          |
| **T06** | PATCH issue status with an invalid value (e.g., `status = Deleted`) | `400 Bad Request`    | `VALIDATION_ERROR` payload.                                                                                 |
| **T07** | PATCH status for an unknown/non-existent issue ID                   | `404 Not Found`      | `ISSUE_NOT_FOUND` error payload.                                                                            |
| **T08** | GET `/api/issues` when no issues exist in data file                 | `200 OK`             | Clean, empty JSON array `[]`.                                                                               |
| **T09** | POST send unexpected extra server-owned fields                      | `201 Created`        | Server ignores client-provided `id`, `status`, or `createdAt` and enforces authoritative server properties. |
