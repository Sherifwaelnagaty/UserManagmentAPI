# Micro Integrator Project

## Overview

This project implements a set of APIs for user management and auditing within a microservice architecture. It includes CRUD operations on user data, logging, auditing of requests and responses, and the implementation of a Swagger API specification. The API also integrates with an API Gateway for additional functionality such as request validation, logging, and schema validation.

---

## Features

### 1. User Management API (CRUD Operations)
This section includes the following endpoints for performing CRUD operations on users:

- **POST /users**: Create a new user.
- **GET /users/{userId}**: Retrieve user information by `userId`.
- **PUT /users/{userId}**: Update existing user information by `userId`.
- **DELETE /users/{userId}**: Delete a user by `userId`.

These endpoints are part of the `user-management` context and perform basic create, read, update, and delete operations on the user entity.

---

### 2. Auditing API
Audit logs are generated for each request, intermediate request, intermediate response, and final response, stored in a table called `Audit`. The following columns are used for logging each request and response:

| Column Name       | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| **CorrelationId**  | Unique request ID that links all related logs.                              |
| **Message**        | The payload of the message.                                                 |
| **FlowType**       | The type of the log entry (e.g., `REQUEST`, `INT_REQUEST`, `RESPONSE`, `INT_RESPONSE`). |
| **ServiceName**    | The name of the service handling the request.                               |
| **Source**         | The source of the request.                                                  |
| **Destination**    | The destination service.                                                   |
| **CreationDate**   | The timestamp when the log entry was created.                               |
| **Param1 to Param5** | Additional parameters used for the audit.                                 |

---

### 3. Swagger Specification
A Swagger API definition is created following standard guidelines. The Swagger file defines the specification for each of the APIs, including request and response formats.

- The API request and response formats, including data types, validation rules, and possible error responses, are fully documented in the Swagger definition.
- Swagger UI is used to provide a user-friendly interface to interact with the API.

---

### 4. Fault Handling and Auditing
In case of errors, a fault sequence will audit the request in both the `Error` table and the `Audit` table, ensuring all failed requests are logged and tracked for troubleshooting.

---

### 5. API Gateway Configuration
This section configures the API Gateway using API Manager.

- **Create API**: The API is created from the Swagger definition within the API Manager.
- **Define Header Mapping**: A custom header `activityid` is defined and mapped to the `requestId` parameter to be passed to the backend API using API policies.
- **Enable Logging**: API logging is enabled using APICTL to track all incoming requests and responses.
- **Enable Schema Validation**: Schema validation is enabled to validate the request body against a predefined schema before passing it to the backend API.
