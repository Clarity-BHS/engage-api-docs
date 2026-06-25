<p align="center">
  <img src="assets/images/engage-logo.png" alt="Engage Logo" width="220">
</p>

<h1 align="center">API Documentation</h1>

# Welcome to the Engage API Documentation

Welcome to the API documentation. This guide provides everything you need to integrate with our REST APIs securely and efficiently.

Our APIs enable authorized applications to exchange data with our platform using standard HTTPS requests and JSON payloads. This documentation includes authentication requirements, request and response formats, endpoint specifications, error handling, and integration best practices.

---

# Environment Variables

The following variables are used throughout this documentation to simplify configuration across environments.

| Variable          | Description                           | Example                              |
| ----------------- | ------------------------------------- | ------------------------------------ |
| `{{base_url}}`    | Base URL for the selected environment | `https://staging.engagebyclarity.com` |
| `{{api_version}}` | Current API version                   | `api/v2`                                 |
| `{{api_key}}`     | API Key issued during onboarding      | `YOUR_API_KEY`                       |

## Environment Configuration

### Sandbox

| Variable      | Value                                |
| ------------- | ------------------------------------ |
| `base_url`    | `https://staging.engagebyclarity.com` |
| `api_version` | `api/v2`                                 |

### Production

| Variable      | Value                        |
| ------------- | ---------------------------- |
| `base_url`    | `https://engagebyclarity.com` |
| `api_version` | `api/v2`                         |

---

# Base URL

All API endpoints are relative to the following URL:

```text
{{base_url}}/{{api_version}}
```

For example, if the endpoint is:

```http
GET /patients
```

The complete request URL becomes:

**Sandbox**

```text
https://staging.engagebyclarity.com/api/v2/patients
```

**Production**

```text
https://engagebyclarity.com/api/v2/patients
```

Using variables, the same request can be represented as:

```text
{{base_url}}/{{api_version}}/patients
```

> **Note**
>
> * All API requests must be made over **HTTPS**.
> * Requests made over **HTTP** are not supported.
> * Future API versions may be introduced by updating the `{{api_version}}` variable.

---

# Authentication

All API requests must be authenticated using an API Key issued during onboarding.

Each client is assigned a unique API key that must be included in the request headers for **every API request**.

Requests that do not include a valid API key will be rejected with an HTTP **401 Unauthorized** response.

## Required Headers

```http
X-API-Key: {{api_key}}
Content-Type: application/json
Accept: application/json
```

### Example Request

```http
GET {{base_url}}/{{api_version}}/patients

X-API-Key: {{api_key}}
Content-Type: application/json
Accept: application/json
```

> **Security Recommendations**
>
> * Keep your API key confidential.
> * Never expose API keys in public repositories or client-side applications.
> * Store API keys securely using environment variables or a secrets management solution.
> * Contact support immediately if your API key is suspected to be compromised.

---

# Request Format

Our APIs follow RESTful conventions.

### Supported HTTP Methods

* GET
* POST
* PUT
* PATCH
* DELETE

### Content Type

Unless otherwise specified, all request payloads must be submitted as JSON.

```http
Content-Type: application/json
Accept: application/json
```

---

# Response Format

All responses are returned in JSON format.

## Successful Response

```json
{
    "success": true,
    "message": "Request completed successfully.",
    "data": {
        ...
    }
}
```

## Error Response

```json
{
    "success": false,
    "message": "Invalid API Key."
}
```

## Validation Error

```json
{
    "success": false,
    "message": "Validation failed.",
    "errors": {
        "field_name": [
            "Validation message."
        ]
    }
}
```

---

# HTTP Status Codes

| Status Code | Description                                    |
| ----------- | ---------------------------------------------- |
| **200**     | Request completed successfully                 |
| **201**     | Resource created successfully                  |
| **204**     | Request completed successfully with no content |
| **400**     | Bad Request                                    |
| **401**     | Unauthorized (Missing or Invalid API Key)      |
| **403**     | Forbidden                                      |
| **404**     | Resource not found                             |
| **409**     | Conflict                                       |
| **422**     | Validation failed                              |
| **429**     | Too Many Requests                              |
| **500**     | Internal Server Error                          |

---

# Best Practices

To ensure a secure and reliable integration:

* Always use HTTPS.
* Include the `X-API-Key` header in every request.
* Validate request payloads before submitting them.
* Handle all HTTP status codes appropriately.
* Never hardcode API credentials in source code.
* Store API credentials securely.
* Implement appropriate timeout and retry mechanisms.
* Keep your integration updated with the latest API version.

---

# Versioning

The API is versioned using the URL path.

```text
{{base_url}}/{{api_version}}
```

Future API versions may introduce additional functionality while maintaining backward compatibility whenever possible.

When a new version becomes available, simply update the `{{api_version}}` variable used in your requests.

---

# Support

If you encounter any issues while integrating with our APIs, please contact our support team.

When raising a support request, include the following information whenever possible:

* Endpoint URL
* HTTP Method
* Request Timestamp
* HTTP Status Code
* Request Body (excluding sensitive information)
* Response Body
* Error Message
* Correlation ID or Request ID (if available)

Providing these details will help us investigate and resolve your issue more efficiently.

---

# Documentation Structure

Each endpoint in this collection includes:

* Endpoint Description
* HTTP Method
* Endpoint URL
* Authentication Requirements
* Request Headers
* Path Parameters
* Query Parameters
* Request Body
* Sample Request
* Success Response
* Error Responses
* HTTP Status Codes
* Business Rules (where applicable)

---

# Getting Started

Before making your first API request, ensure you have:

* Access to the appropriate environment (Sandbox or Production).
* A valid API Key.
* An HTTP client such as Postman, Insomnia, cURL, or your preferred programming language.
* Network access to the API endpoint.

Once configured, you're ready to begin integrating with the available API endpoints documented in this collection.

---

# Changelog

Changes to the API will be communicated through version updates and release notes.

We recommend reviewing the documentation periodically to stay informed about new features, enhancements, and deprecations.
