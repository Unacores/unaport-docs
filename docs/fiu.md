<script>
function openTab(evt, tabName) {
  var i, tabcontent, tablinks;
  tabcontent = document.getElementsByClassName("tabcontent");
  for (i = 0; i < tabcontent.length; i++) {
    tabcontent[i].style.display = "none";  
  }
  tablinks = document.getElementsByClassName("tablink");
  for (i = 0; i < tablinks.length; i++) {
    tablinks[i].className = tablinks[i].className.replace(" active", "");
  }
  document.getElementById(tabName).style.display = "block";  
  evt.currentTarget.className += " active";
}

/* Light green background for footnotes */
.footnote-ref, .footnote {
    background-color: #e0f7e9; /* light green color */
    padding: 5px;
    border-radius: 3px;
}

</script>


!!! note "🚀 API Version Update - v2.0.0 🚀"
    **📅 Release Date:** *15th November 2024*

    We’re thrilled to announce the launch of **Unaport FIU API v2.0.0**!  
    👉 **New consumers, please use this version to access the latest features and improvements.**

    <div class="line"></div>

    🎯 **Get started now!**  

    <a href="https://unacores.github.io/unaport-docs/json/postman.json" class="download-button" download>
        ⬇️ **Postman Collection v2.0**
    </a>

    <a href="https://unacores.github.io/unaport-docs/json/Unaport.postman_environment.json"  download Environment>
        **Download Environment Variables**
    </a>

      *(Ensure you whitelist the following Unaport IP addresses for notifications:)*  - **UAT**: `15.206.247.111` **Production**: `13.234.23.251`  

## 🌟 **Introduction**  

To start with the integration, follow the steps below:  

# 🔗 **Unaport.ai API**  

Welcome to the **Unaport.ai API Reference**!  
This guide provides everything you need to integrate Unaport.ai services into your application, including:  

- Generating user consent  
- Retrieving user details  
- Accessing analyzed data and CAM sheets  

The Unaport.ai APIs are fully RESTful, and all responses are delivered in **JSON** format.  

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/selection.png" alt="Dashboard" width="700">
</p>  

---

### 🔐 **Authentication**  

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/Login.png" alt="Dashboard" width="500">
</p>  

1. **Login API**: Authenticate requests using the Bearer token obtained via the Login API.  
2. **Refresh Token API**: Get a new access token with a valid refresh token.  
3. **Get Organisation Details API**: Retrieve organizational details such as name, type, and contact information.  

---

### 📝 **Consents Description**  

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/Consents.png" alt="Consents" width="400">
</p>  

4. **Create Consent Template API**: Create standardized consent templates with parameters like purpose, data types, and expiration.  
5. **Get Consent Templates List API**: View and manage predefined templates.  
6. **Create Consent without Template API**: Customize consent requests without using templates.  
7. **Create Consent with Template API**: Generate consent requests based on predefined templates.  
8. **Check Consent Status API**: Verify the status and details of a specific consent request.  
9. **Revoke Consent API**: FIUs can revoke already approved consent status.  
10. **Consent Notification API**: Notify FIUs about consent status changes.  

---

### 📊 **Data Reports Description**  

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/Data.png" alt="Data" width="300">
</p>  

10. **Fetch Data Status API**: Check the status of data sharing for a consent handle.  
11. **Fetch Data API**: Retrieve session-specific data using a session ID.  
12. **Export Data API**: Export session-specific data.  
13. **Data Notification API**: Notify FIUs/AA clients about Financial Information fetch statuses.  

---

### 📈 **Analytics Description**  

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/analytics.png" alt="Analytics" width="300">
</p>  

14. **Generate Analytics API**: Create detailed analytical reports.  
15. **Get Account Details API**: Retrieve account information, including balance and transactions.  
16. **Fetch Analytics API**: Retrieve analytics data for a specific analytic ID.  
17. **Export Analytics API**: Export detailed analytics data.  

---

## 🛠️ **Response Status Codes**  

API responses are communicated via HTTP using the following status codes:  

- **200: OK** – Successful request.  
- **201: Created** – New resource created.  
- **400: Bad Request** – Invalid request, often due to missing parameters.  
- **401: Unauthorized** – No valid API key provided.  
- **403: Forbidden** – Insufficient permissions.  
- **500: Server Errors** – Issue on Unaport.ai's server.  

---


### Login

All the API requests are authenticated using the Bearer token. To get this token, you will need to make a request to the login API using the credentials. The response will contain the token. Send the token in the header for all the requests.

#### Request Table

| Attribute   | Description                | Length | Datatype | Mandatory/Optional | 
|-------------|----------------------------|--------|----------|---------------------|
| `emailId`   | User's email address       | 254    | String   | Mandatory          |
| `password`  | User's password for login  | 8-64   | String   | Mandatory          |

#### Response Table

| Attribute            | Description                                            | Type   |
|----------------------|--------------------------------------------------------|--------|
| `timestamp`          | The timestamp of the response                          | String |
| `txnId`              | Unique transaction identifier                          | String |
| `version`            | API version                                            | String |
| `access_token`       | Access token for the authenticated user                | String |
| `expires_in`         | Duration (in seconds) before the access token expires  | Number |
| `refresh_expires_in` | Duration (in seconds) before the refresh token expires | Number |
| `refresh_token`      | Token used to refresh the access token                 | String |
| `token_type`         | Type of token, typically "Bearer"                      | String |

### Refresh Token API 

Allows users to obtain a new access token by providing a valid refresh token. This ensures continued access to secured resources without requiring the user to re-authenticate, enhancing user experience and maintaining session continuity.

### Request Table


| Attribute       | Description                      | Length | Datatype | Mandatory/Optional |
|-----------------|----------------------------------|--------|----------|---------------------|
| `refresh_token` | The refresh token for renewing access | 255    | String   | Mandatory          |

### Response Table

| Attribute            | Description                                            | Type   |
|----------------------|--------------------------------------------------------|--------|
| `timestamp`          | The timestamp of the response                          | String |
| `txnId`              | Unique transaction identifier                          | String |
| `version`            | API version                                            | String |
| `access_token`       | Access token for the authenticated user                | String |
| `expires_in`         | Duration (in seconds) before the access token expires  | Number |
| `refresh_expires_in` | Duration (in seconds) before the refresh token expires | Number |
| `refresh_token`      | Token used to refresh the access token                 | String |
| `token_type`         | Type of token, typically "Bearer"                      | String |

### Get FIU Organisation Details API

The API retrieves information about a specific organization using its unique identifier. It provides essential details such as the organization's name, type, and contact information, enabling users to access relevant organizational data

### Request Table

- **URL:** `https://common.sandbox.unaport.com/api/v1/FIU/getClientOrganisation`
- **HTTP Method:** `GET` 
- **Headers:**
  - **Authorization:** Bearer token for authenticating the request.
  - **Content-Type:** Specifies the request body format (JSON).

### Response Table

| Attribute   | Description                                            | Type   |
|-------------|--------------------------------------------------------|--------|
| `ver`       | API version                                            | String |
| `fiulive`   | Live FIU entity information                            | Object |
| `entityId`  | Identifier of the FIU entity in live mode              | String |
| `id`        | Unique identifier for the FIU entity in live mode      | String |
| `fiutest`   | Test FIU entity details                                | Object |
| `entityId`  | Identifier of the FIU entity in test mode              | String |
| `id`        | Unique identifier for the FIU entity in test mode      | String |
| `orgId`     | Organization identifier                                | String |
| `timestamp` | The timestamp of the response                          | String |
| `txnId`     | Unique transaction identifier                          | String |

<div class="line"></div>

### Consents

### Create Consent Template API

The enables users to create a standardized consent template for data sharing among service providers. By defining parameters such as purpose, data types, and expiration, it streamlines the consent management process, ensuring compliance and clarity in user agreements.

### Request Table
| Attribute                          | Description                                                                                          | Length | Datatype | Mandatory/Optional |
|------------------------------------|------------------------------------------------------------------------------------------------------|--------|----------|---------------------|
| `product_name`                     | Name of the product to be inserted                                                                   | 100    | String   | Mandatory          |
| `ConsentDetail`                    | Contains details of the user’s consent                                                               | -      | Object   | Mandatory          |
| `ConsentDetail.consentStart`       | Start date for consent in ISO 8601 format                                                            | 20     | String   | Mandatory          |
| `ConsentDetail.consentExpiry`      | Duration until consent expires, in months - `12`                                                     | 2      | String   | Mandatory          |
| `ConsentDetail.consentMode`        | Enum for the type of consent. Possible values are `VIEW`, `STORE`, `QUERY`, `STREAM`                 | 10     | String   | Mandatory          |
| `ConsentDetail.fetchType`          | Enum to specify either `ONETIME` or `PERIODIC` fetch of data                                         | 8      | String   | Mandatory          |
| `ConsentDetail.consentTypes`       | Types of consent requested, e.g., `PROFILE`, `SUMMARY`, `TRANSACTIONS`                               | 15      | String    | Mandatory          |
| `ConsentDetail.fiTypes`            | Types of financial information, e.g., [FI Types](#fi-types)                                         | 15      | String    | Mandatory          |
| `ConsentDetail.DataConsumer.id`    | ID of the FIU                                                                                        | 50     | String   | Mandatory          |
| `ConsentDetail.Purpose.code`       | Purpose code of the consent - [Purpose Code Definition](#purpose-code-definition)                    | 10     | String   | Mandatory          |
| `ConsentDetail.Purpose.refUri`     | Reference URI for purpose definition - `https://api.rebit.org.in/aa/purpose/101.xml`                 | 255    | String   | Optional           |
| `ConsentDetail.Purpose.text`       | Text description of the purpose, e.g., `Wealth management service`                                   | 255    | String   | Optional           |
| `ConsentDetail.Purpose.Category.type` | Category type of the purpose, e.g., `Personal Finance`                                             | 50     | String   | Optional           |
| `ConsentDetail.FIDataRange.from`   | Start of the data range in months, negative for past dates - `-12`                                   | 4      | Number   | Mandatory          |
| `ConsentDetail.FIDataRange.to`     | End of the data range in months - `12`                                                               | 4      | Number   | Mandatory          |
| `ConsentDetail.DataLife.unit`      | Time period for data storage. Options: `MONTH`, `YEAR`, `DAY`, `INF`                                 | 5      | String   | Mandatory          |
| `ConsentDetail.DataLife.value`     | Value defining the duration for data life - `1`                                                      | 3      | Number   | Mandatory          |
| `ConsentDetail.Frequency.unit`     | Frequency unit for data refresh, e.g., `HOUR`, `MONTH`, `YEAR`, `DAY`, `INF`                         | 5      | String   | Mandatory          |
| `ConsentDetail.Frequency.value`    | Frequency value for data refresh, e.g., `1`                                                          | 3      | Number   | Mandatory          |
| `ConsentDetail.DataFilter`         | Conditions for filtering the data being fetched                                                      | -      | Array    | Optional           |

#### Purpose Code Definition

| Code | Service Description                                      | Category Code | Category                     |
|------|----------------------------------------------------------|---------------|-------------------------------|
| 101  | Wealth management service                                | 01            | Personal Finance              |
| 102  | Customer spending patterns, budget or other reportings   | 01            | Personal Finance              |
| 103  | Aggregated statement                                     | 02            | Financial Reporting           |
| 104  | Explicit consent for monitoring of the accounts          | 03            | Account Query and Monitoring  |
| 105  | Explicit one-time consent for the accounts               | 03            | Account Query and Monitoring  |

#### FI TYPES

| Category    | FI Types                                 |
|-------------|------------------------------------------|
| Bank        | DEPOSIT, TERM_DEPOSIT, RECURRING_DEPOSIT |
| Investment  | MUTUAL_FUNDS, ETF, EQUITIES, NPS         |
| Insurance   | INSURANCE_POLICIES                       |
| GST         | GSTR1_3B                                 |


<a id="consent-overview"></a> <!-- This adds an anchor -->

#### Consent Relationship Overview

The relationship between the consent status, consent handle, and consent ID for AA, FIP, and FIU is depicted in the table below:

| **Use Case**                                    | **Status**   | **Notification Sender** | **Notification Receiver** | **Consent Id** | **Consent Handle** |
|-------------------------------------------------|--------------|--------------------------|----------------------------|----------------|---------------------|
| **Consent Approval Status**                             |              |                          |                            |                |                     |
| Consent Request raised by FIU                   | PENDING      | AA                       | Customer                   | Null           | Available           |
| Customer rejects the consent at AA Client       | FAILED     | AA                       | FIU                        | Null           | Available           |
| Consent is approved/paused/revoked by customer                 | READY     | AA                       | FIU, FIP                   | Available      | Available           |
| Consent request is expired at AA                | EXPIRED      | AA                       | FIU                        | Null           | Available           |
| **Consent Status**                            |              |                          |                            |                |                     |
| Consent Request raised by FIU                 | CREATED       | AA                       | Customer                   | Null      | Available           |
| Consent is approved by customer                 | ACTIVE       | AA                       | FIU, FIP                   | Available      | Available           |
| Customer revokes the consent using AA client    | REVOKED      | AA                       | FIU, FIP                   | Available      | Available           |
| Customer initiates revoke consent from FIP      | REVOKED      | FIP                      | AA                         | Available      | NA                  |
| AA processes the consent revocation from FIP    | REVOKED      | AA                       | FIU, FIP, Customer         | Available      | Available           |
| FIU sends consent revocation request to AA      | REVOKED      | FIU                      | AA                         | Available      | Available           |
| AA processes the revocation request from FIU    | REVOKED      | AA                       | FIU, FIP, Customer         | Available      | Available           |
| Customer pauses the consent using AA client     | PAUSED       | AA                       | FIU, FIP                   | Available      | Available           |
| Customer resumes the consent using AA client    | ACTIVE       | AA                       | FIU, FIP                   | Available      | Available           |
| Consent is expired at AA                        | EXPIRED      | AA                       | FIU, FIP                   | Available      | Available           |

#### Additional Notes

- **Consent Handle**: Available with AA throughout the consent lifecycle.  
- **Consent ID**: Generated by AA only after the consent is approved by the customer.  

### Key Points:
1. **FIP**: Receives the consent artefact only after approval by the customer. FIP uses the **Consent ID** for communication with AA.  
2. **FIU and AA**: May have both **Consent Handle** and **Consent ID** values depending on the consent artefact status.


### Response Table

| Attribute     | Description                          | Type   |
|---------------|--------------------------------------|--------|
| `version`     | API version                          | String |
| `txnId`       | Unique transaction identifier        | String |
| `productId`   | Product identifier                   | String |
| `productName` | Name of the product                  | String |
| `timestamp`   | The timestamp of the response        | String |

### Create Consent API without template

The API allows users to generate a new consent request independently of predefined templates. This provides flexibility for users to define specific parameters, such as data types and sharing purposes, facilitating customized consent agreements tailored to unique data-sharing scenarios.

| Attribute                   | Description                                                                                              | Length | Datatype | Mandatory/Optional |
|-----------------------------|----------------------------------------------------------------------------------------------------------|--------|----------|---------------------|
| `vuaId`                     | Virtual User ID representing the user within the consent framework                                       | 50     | String   | Mandatory          |
| `createdBy`                 | Email of the user or developer initiating the consent request                                            | 100    | String   | Mandatory          |
| `trackingId`                | Tracking identifier for the consent request                                                              | 50     | String   | Mandatory          |
| `aaId`                      | Account Aggregator identifier for the request                                                            | 50     | String   | Mandatory          |
| `fiuId`                     | Financial Information User identifier                                                                   | 50     | String   | Mandatory          |
| `redirectUrl`               | URL to redirect after consent is processed                                                               | 255    | String   | Optional           |
| `fiuBaseUrl`                | Base URL for the Financial Information User API                                                          | 255    | String   | Mandatory          |
| `ConsentsRequest`           | Main object containing details of the consent request                                                    | -      | Object   | Mandatory          |
| ├─ `ver`                    | Version of the consent request                                                                           | 5      | String   | Mandatory          |
| ├─ `timestamp`              | Timestamp of the consent request                                                                         | 25     | String   | Mandatory          |
| ├─ `txnid`                  | Transaction ID associated with the request                                                               | 50     | String   | Mandatory          |
| ├─ `ConsentDetail`          | Details of the consent                                                                                   | -      | Object   | Mandatory          |
| │  ├─ `consentStart`        | Start date-time of the consent (e.g., 2019-12-06T11:39:57.153Z)                                         | 24     | String   | Mandatory          |
| │  ├─ `consentExpiry`       | Expiry date-time for the consent (e.g., 2019-12-06T11:39:57.153Z)                                       | 24     | String   | Mandatory          |
| │  ├─ `consentMode`         | Mode of consent. Possible values are `VIEW`, `STORE`, `QUERY`, `STREAM`                                 | 10     | String   | Mandatory          |
| │  ├─ `fetchType`           | Enum to specify either `ONETIME` or `PERIODIC` fetch of data                                            | 8      | String   | Mandatory          |
| │  ├─ `consentTypes`        | List of consent types (e.g., `PROFILE`, `SUMMARY`, `TRANSACTIONS`)                                      | -      | Array    | Mandatory          |
| │  ├─ `fiTypes`             | List of Financial Information types (e.g., [FI Types](#fi-types))                                       | -      | Array    | Mandatory          |
| │  ├─ `DataConsumer`        | Information about the consumer of the data                                                               | -      | Object   | Mandatory          |
| │  │  ├─ `id`               | Identifier of the FIU                                                                                   | 50     | String   | Mandatory          |
| │  │  ├─ `type`             | Type of data consumer (e.g., `FIU`)                                                                      | 10     | String   | Mandatory          |
| │  ├─ `Customer`            | Details of the customer associated with the consent                                                     | -      | Object   | Mandatory          |
| │  │  ├─ `id`               | Identifier of the Customer (e.g., customer_identifier@AA_identifier)                                    | 100    | String   | Mandatory          |
| │  │  ├─ `Identifiers`      | List of identifiers for the customer (e.g., mobile number)                                              | -      | Array    | Optional           |
| │  ├─ `Purpose`             | Purpose of the data sharing                                                                             | -      | Object   | Mandatory          |
| │  │  ├─ `code`             | Purpose code (e.g., `103`)                                                                              | 10     | String   | Mandatory          |
| │  │  ├─ `refUri`           | Reference URI for purpose                                                                               | 255    | String   | Optional           |
| │  │  ├─ `text`             | Text description of the purpose                                                                         | 255    | String   | Optional           |
| │  │  ├─ `Category`         | Category for the purpose                                                                                | -      | Object   | Optional           |
| │  │  │  ├─ `type`          | Type of category (e.g., `Financial Reporting`)                                                          | 50     | String   | Optional           |
| │  ├─ `FIDataRange`         | Date range for the financial information                                                                | -      | Object   | Mandatory          |
| │  │  ├─ `from`             | Start date of the data range                                                                            | 24     | String   | Mandatory          |
| │  │  ├─ `to`               | End date of the data range                                                                              | 24     | String   | Mandatory          |
| │  ├─ `DataLife`            | Duration of data availability                                                                           | -      | Object   | Mandatory          |
| │  │  ├─ `unit`             | Unit of time for data life (e.g., `MONTH`, `YEAR`, `DAY`, `INF`)                                       | 5      | String   | Mandatory          |
| │  │  ├─ `value`            | Value associated with the data life unit                                                                | 3      | Integer  | Mandatory          |
| │  ├─ `Frequency`           | Frequency of data sharing                                                                               | -      | Object   | Mandatory          |
| │  │  ├─ `unit`             | Unit of frequency (e.g., `HOUR`, `DAY`, `MONTH`, `YEAR`, `INF`)                                        | 5      | String   | Mandatory          |
| │  │  ├─ `value`            | Value associated with the frequency unit                                                                | 3      | Integer  | Mandatory          |

### Response Table

| Attribute       | Description                                      | Type   |
|-----------------|--------------------------------------------------|--------|
| `ver`           | API version                                      | String |
| `timestamp`     | The timestamp of the response                    | String |
| `txnid`         | Unique transaction identifier                    | String |
| `Customer`      | Customer details                                 | Object |
| `id`            | Customer identifier                              | String |
| `ConsentHandle` | Unique identifier for the consent handle         | String |
| `success`       | Status message indicating success of the action  | String |
| `redirectUrl`   | URL for redirecting after consent creation       | String |

### Create Consent with Template API

This API allows users to generate a new consent request based on a predefined template. By leveraging existing templates, users can ensure compliance and consistency in consent agreements while easily specifying the relevant data types and sharing purposes for the intended data-sharing scenario.

### Request Table

| Attribute      | Description                                                      | Length | Datatype | Mandatory/Optional |
|----------------|------------------------------------------------------------------|--------|----------|---------------------|
| `vuaId`        | User’s unique identifier for AA (Account Aggregator)             | 50     | String   | Mandatory          |
| `mobileNumber` | The mobile number associated with the consent request            | 15     | String   | Mandatory          |
| `createdBy`    | The email address of the person or system creating the consent   | 100    | String   | Mandatory          |
| `trackingId`   | Unique ID used to track the consent request                      | 50     | String   | Mandatory          |
| `aaId`         | The ID of the Account Aggregator initiating the consent request  | 50     | String   | Mandatory          |
| `fiuId`        | The ID of the Financial Information User (FIU)                   | 50     | String   | Mandatory          |
| `redirectUrl`  | URL where the user will be redirected after consent is given     | 255    | String   | Optional           |
| `fiuBaseUrl`   | The base URL of the FIU API                                      | 255    | String   | Mandatory          |
| `productId`    | The ID of the product for which consent is requested             | 50     | String   | Mandatory          |

### Response Table

| Attribute       | Description                                      | Type   |
|-----------------|--------------------------------------------------|--------|
| `ver`           | API version                                      | String |
| `timestamp`     | The timestamp of the response                    | String |
| `txnid`         | Unique transaction identifier                    | String |
| `Customer`      | Customer details                                 | Object |
| `id`            | Customer identifier                              | String |
| `ConsentHandle` | Unique identifier for the consent handle         | String |
| `success`       | Status message indicating success of the action  | String |
| `redirectUrl`   | URL for redirecting after consent creation       | String |

### Check Consent Status API

The API allows users to verify the status and details of a specific consent request using its unique consent handle. This enables users to retrieve information about the consent's validity, scope, and associated data-sharing agreements, ensuring transparency and control over consented data access.

### Header Table

| **Attribute**     | **Description**                                                      | **Type**      |
|-------------------|----------------------------------------------------------------------|---------------|
| `Authorization`   | Bearer token for authenticating the API request.                     | String (Bearer Token) |
| `Data`            | Empty request body, as this is a `GET` request.                      | N/A (Empty Body) |

### Response Table

| **Attribute**      | **Description**                                                      | **Type**      |
|--------------------|----------------------------------------------------------------------|---------------|
| `Data`             | Array of consent records.                                             | Array         |
| `id`               | The unique identifier for the consent record.                        | Integer       |
| `trackingId`       | The tracking ID for the consent request.                             | String        |
| `vuaId`            | The ID of the user requesting consent.                               | String        |
| `orgId`            | The ID of the organization associated with the consent.              | String        |
| `consentHandle`    | The unique handle for the consent.                                   | String        |
| `approveStatus`    | The approval status of the consent.                                  | String        |
| `consentStatus`    | The current status of the consent (e.g., ACTIVE, INACTIVE).          | String        |
| `fetchType`        | The type of consent (e.g., `ONETIME`).                               | String        |
| `consentId`        | The unique consent ID associated with the consent.                   | String        |
| `createdAt`        | The timestamp when the consent was created.                          | String (ISO 8601) |
| `notificationDate` | The date when the consent notification was sent.                     | String (ISO 8601) |
| `consentStart`     | The start date of the consent validity period.                       | String (ISO 8601) |
| `consentExpried`   | The expiration date of the consent.                                  | String (ISO 8601) |
| `lastRuntime`      | The last time the consent was executed.                              | String (ISO 8601) |
| `nextRuntime`      | The next time the consent is expected to be executed.                | String (ISO 8601 or null) |
| `updatedOn`        | The timestamp when the consent was last updated.                     | String (ISO 8601 or null) |
| `createdBy`        | The user who created the consent.                                    | String        |
| `aaId`             | The Account Aggregator ID associated with the consent.              | String        |
| `consentsDetail`   | A detailed JSON string of the consent.                               | String (JSON) |
| `signedConsent`    | The signed consent token.                                            | String        |
| `consentidCalled`  | The count of times the consent was called.                           | Integer       |
| `runCounter`       | The run counter for the consent.                                     | Integer       |
| `consentidError`   | Any error associated with the consent call.                          | Null / String |


### Revoke Consent 

This API allows users to revoke a already approved consent request.

#### Path Parameters:
| **Parameter** | **Description**                 | **Type**   |
|---------------|---------------------------------|------------|
| `org_id`      | The unique identifier of the organization. | String    |
| `consentId`   | The unique identifier of the consent to be revoked. | String |


### Consent-Notification-API

This API is intended to be used by AA to notify FIU about the change in consent status due to the consent management operations performed by the Customer.

FIU need to implement on your server and expose to receive notifications from Unaport.ai. These notifications are webhooks from Unaport based on the events that occur during the consent and data flow.

The base_url is the server URL you share with us to receive notifications.

### Request Body

Here's the table reflecting the attributes from the provided output:

| **Attribute**                  | **Description**                     | **Type**       |
|--------------------------------|-------------------------------------|----------------|
| `ver`                          | Version of the notification         | String         |
| `timestamp`                    | Timestamp of the notification       | ISO 8601 DateTime |
| `txnid`                        | Unique transaction ID               | UUID           |
| `Notifier.type`                | Type of the notifier (e.g., `AA`)   | String         |
| `Notifier.id`                  | Identifier for the notifier         | String         |
| `ConsentStatusNotification.consentId` | ID of the consent                    | String         |
| `ConsentStatusNotification.consentHandle` | Handle associated with the consent  | String         |
| `ConsentStatusNotification.consentStatus` | Status of the consent (`PAUSED`)   | String         |


<div class="line"></div>

### Data

### Data-Notification-API

This API can be used by AAs to send notifications related to Financial Information (FI) fetch to FIU/AA Client.

FIU need to implement on your server and expose to receive notifications from Unaport.ai. These notifications are webhooks from Unaport based on the events that occur during the consent and data flow.

The base_url is the server URL you share with us to receive notifications.

### Request Body

Here’s the table representation of the provided JSON structure:

| **Key**                  | **Description**                                             | **Value/Type**            |
|--------------------------|-------------------------------------------------------------|---------------------------|
| `ver`                    | API version                                                 | `2.0.0` (String)          |
| `timestamp`              | Timestamp of the response                                   | `2023-06-26T11:39:57.153Z` (String) |
| `txnid`                  | Unique transaction identifier                               | `0b811819-9044-4856-b0ee-8c88035f8858` (String) |
| `Notifier`               | Notifier details                                            | Object                    |
| `Notifier.type`          | Type of notifier                                            | `AA` (String)             |
| `Notifier.id`            | Notifier identifier                                         | `AA-1` (String)           |
| `FIStatusNotification`   | Financial Information (FI) status notification details     | Object                    |
| `FIStatusNotification.sessionId` | Session identifier                                   | `XXXX0-XXXX-XXXX` (String) |
| `FIStatusNotification.sessionStatus` | Current session status                          | `ACTIVE` (String)         |
| `FIStatusNotification.FIStatusResponse` | List of FI status responses                  | Array                     |
| `FIStatusResponse[0].fipID` | Financial Information Provider (FIP) ID                   | `FIP-1` (String)          |
| `FIStatusResponse[0].Accounts` | List of accounts for the FI                           | Array                     |
| `Accounts[0].linkRefNumber` | Account reference number                                  | `XXXX-XXXX-XXXX` (String) |
| `Accounts[0].FIStatus`   | Financial information status                                | `READY` (String)          |
| `Accounts[0].description`| Additional details or description                           | Empty string (`""`)       |

### Fetch Data Status API

This API enables users to retrieve the current status of data sharing associated with a specific consent handle. This API provides insights into whether the consent is active, the data requested, and any updates on the data-sharing process, ensuring users can monitor and manage their consented data effectively.

### Header Table


| **Attribute**     | **Description**                                                      | **Type**      |
|-------------------|----------------------------------------------------------------------|---------------|
| `Authorization`   | Bearer token for authenticating the API request.                     | String (Bearer Token) |
| `Data`            | Empty request body, as this is a `GET` request.                      | N/A (Empty Body) |

### Response Table

| **Attribute**                     | **Description**                                              | **Type**         |
|-----------------------------------|--------------------------------------------------------------|------------------|
| `data`                            | Array containing FIU notification details.                   | Array            |
| `ver`                             | API version used for the notification.                       | String           |
| `timestamp`                       | Timestamp of the notification.                               | String (ISO 8601) |
| `txnid`                           | Unique transaction ID for the notification.                  | String           |
| `Notifier.type`                   | Type of notifier (e.g., `AA` for Account Aggregator).        | String           |
| `Notifier.id`                     | ID of the notifier (Account Aggregator ID).                  | String           |
| `FIStatusNotification.sessionId`   | Session ID associated with the notification.                 | String           |
| `FIStatusNotification.sessionStatus` | Status of the session (e.g., `COMPLETED`).                   | String           |
| `FIStatusNotification.FIStatusResponse` | Array containing financial institution status responses. | Array            |
| `FIStatusResponse.fipID`          | Financial institution provider ID.                           | String           |
| `FIStatusResponse.Accounts`       | Array of account statuses for the financial institution.     | Array            |
| `Accounts.linkRefNumber`          | Link reference number associated with the account.           | String           |
| `Accounts.FIStatus`               | Status of financial information readiness (e.g., `READY`).   | String           |
| `Accounts.description`            | Description of the FI status.                                | String           |
| `status`                          | Overall status of the notification (e.g., `success`).        | String           |


### Fetch Data API

This allows users to retrieve data associated with a specific session identified by its unique session ID. This API provides access to the relevant information tied to the session, enabling users to track and manage data interactions seamlessly within their established sessions.

### Header Table

| **Attribute**       | **Description**                                                      | **Type**               |
|---------------------|----------------------------------------------------------------------|------------------------|
| `Authorization`     | Bearer token for authenticating the API request.                     | String (Bearer Token)  |
| `sessionId`         | Unique session identifier for fetching financial data.               | Path Parameter         |

### Response Table

| **Attribute**                       | **Description**                                                  | **Type**           |
|-------------------------------------|------------------------------------------------------------------|--------------------|
| `version`   | API version                          | String |
| `txnId`     | Unique transaction identifier        | String |
| `timestamp` | The timestamp of the response        | String |
| `tabs`                              | Array of tab names for different financial data types.           | Array of Objects   |
| `tabs.name`                         | Type of financial information (e.g., "DEPOSIT").                 | String             |
| `DEPOSIT`                           | Contains summary, account holder, and transaction details.       | Object             |

---

### `DEPOSIT` Object

#### Summary Details

| **Attribute**                  | **Description**                                               | **Type**           |
|--------------------------------|---------------------------------------------------------------|--------------------|
| `id`                            | Unique ID (can be null if not provided).                      | String or Null     |
| `currentBalance`                | Current balance of the account.                               | String             |
| `orgId`                         | Unique organization identifier.                               | String             |
| `branch`                        | Branch code of the account.                                   | String             |
| `status`                        | Status of the account (e.g., `ACTIVE`).                       | String             |
| `currency`                      | Currency in which the account operates (e.g., `INR`).         | String             |
| `fip`                            | Financial institution provider ID.                            | String             |
| `accountNumber`                 | Masked account number.                                        | String             |
| `sessionId`                     | Unique session identifier.                                    | String             |
| `createdAt`                     | Timestamp when the account was created.                       | String (ISO 8601)  |
| `facility`                      | Type of facility (e.g., `OD` for Overdraft).                  | String             |
| `ifscCode`                      | IFSC code of the branch.                                      | String             |
| `microCode`                     | Micro Code of the branch.                                     | String             |
| `openingDate`                   | Date when the account was opened.                             | String (YYYY-MM-DD)|
| `currentOdLimit`                | Current overdraft limit (if applicable).                      | String             |
| `drawingLimit`                  | Current drawing limit.                                        | String             |
| `accountType`                   | Type of account (e.g., `SAVINGS`).                            | String             |

#### Account Holder Details

| **Attribute**                  | **Description**                                               | **Type**           |
|--------------------------------|---------------------------------------------------------------|--------------------|
| `name`                          | Name of the account holder.                                   | String             |
| `dob`                           | Date of birth of the account holder.                          | String (YYYY-MM-DD)|
| `nominee`                       | Nominee status (e.g., `REGISTERED`).                          | String             |
| `email`                         | Email of the account holder.                                  | String             |
| `pan`                           | PAN number of the account holder.                             | String             |
| `address`                       | Residential address of the account holder.                    | String             |
| `mobile`                        | Mobile number of the account holder.                          | String             |
| `fetchType`                     | Type of fetch (e.g., `deposit`).                              | String             |
| `accountHoldertype`             | Account holder type (e.g., `SINGLE`).                         | String             |
| `ckycCompliance`                | CKYC compliance status.                                       | String             |

#### Transactions

| **Attribute**                  | **Description**                                               | **Type**           |
|--------------------------------|---------------------------------------------------------------|--------------------|
| `tranTimestamp`                 | Timestamp of the transaction.                                 | String (ISO 8601)  |
| `narration`                     | Description or note for the transaction.                      | String             |
| `amount`                        | Transaction amount.                                           | String             |
| `type`                          | Type of transaction (`DEBIT` or `CREDIT`).                    | String             |
| `mode`                          | Transaction mode (e.g., `OTHERS`).                            | String             |
| `currentBalance`                | Balance after the transaction.                                | String             |
| `txnId`                         | Unique transaction ID.                                        | String             |
| `reference`                     | Reference number for the transaction.                         | String             |

<div class="line"></div>

### Analytics

### Generate Analytics API - ( Sync & ASync)

The API allows users to create detailed analytical reports based on the activities and data interactions associated with a specific session identified by its session ID. This API provides insights into user behavior, data usage patterns, and overall engagement, helping organizations make informed decisions and optimize their services.

### Header Table

| **Attribute**       | **Description**                                                         | **Type**               |
|---------------------|-------------------------------------------------------------------------|------------------------|
| `Authorization`     | Bearer token for authenticating the API request.                        | String (Bearer Token)  |
| `sessionId`         | Unique session identifier used to fetch analytics data.                 | Path Parameter         |
| `reportId`          | Static part of the endpoint that appears before the `sessionId`         | String (UUID)          |

### Response Structure

| **Attribute**       | **Description**                                           | **Type**       |
|---------------------|-----------------------------------------------------------|----------------|
| `reportId`          | Unique identifier for the analytics report.               | String (Integer)  |
| `status`            | HTTP status code indicating the success of the request.   | String         |


### Analytics-Notification-Api

The Analytics Notification API is designed to notify the client about the status and details of analytics-related sessions and transactions. This API provides critical information regarding the progress and success of analytic operations, including unique identifiers for tracking, timestamps for accurate logging, and session information for context.

| **Key**          | **Description**                           | **Value/Type**                      |
|-------------------|-------------------------------------------|-------------------------------------|
| `version`         | API version                              | `2.0.0` (String)                   |
| `txnId`           | Unique transaction identifier            | `85939887-8067-491f-8149-c90b054ff0ee` (String) |
| `timestamp`       | Timestamp of the response                | `2024-11-20T09:31:59.801Z` (String) |
| `sessionId`       | Unique session identifier                | `248c487f-fd9e-4522-9fb6-c50af4dbcb5f` (String) |
| `analyticId`      | List of analytic IDs                     | `[524]` (Array of integers)         |
| `status`          | Status of the operation                  | `SUCCESS` (String)                  |