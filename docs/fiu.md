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
</script>

# <span style="color: #2c3e50;">Unaport.ai API</span>

Welcome to the **Unaport.ai API Reference**. This guide provides all the information you need to integrate Unaport.ai services into your application, including generating user consent, retrieving user details, and accessing analyzed data and CAM sheets. The Unaport.ai APIs are fully RESTful, and all responses are delivered in JSON format.

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/selection.png" alt="Dashboard" width="700">
</p>

## <span style="color: #2980b9;">Introduction</span>

To start with the integration, follow the steps below:

### <span style="color: #3498db;">Authentication</span>

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/Login.png" alt="Dashboard" width="500">
</p>

1. **Login API**: All API requests are authenticated using the Bearer token. Make a request to the login API with your credentials to obtain this token. Send it in the header for all requests.
2. **Refresh Token API**: Obtain a new access token by providing a valid refresh token, allowing users to maintain access to secured resources.
3. **Get Organisation Details API**: Retrieves information about a specific organization, including its name, type, and contact information.

### <span style="color: #3498db;">Consents</span>

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/Consents.png" alt="Dashboard" width="400">
</p>

4. **Create Consent Template API**: Enables users to create a standardized consent template, defining parameters like purpose, data types, and expiration.
5. **Get Consent Templates List API**: Retrieves available consent templates, allowing users to view and manage predefined templates.
6. **Create Consent without Template API**: Allows creation of a new consent request without predefined templates, supporting customized consent agreements.
7. **Create Consent with Template API**: Generate consent requests based on predefined templates, ensuring compliance and consistency.
8. **Check Consent Status API**: Verify the status and details of a specific consent request using its unique consent handle.

### <span style="color: #3498db;">Data Reports</span>

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/Data.png" alt="Dashboard" width="300">
</p>

9. **Fetch Data Status API**: Retrieve the current status of data sharing associated with a consent handle.
10. **Fetch Data API**: Retrieve data associated with a specific session, identified by its session ID.

### <span style="color: #3498db;">Analytics</span>

<p align="center">
  <img src="https://unacores.github.io/unaport-docs/images/analytics.png" alt="Dashboard" width="300">
</p>

11. **Generate Analytics API**: Create detailed analytical reports based on activities within a session.
12. **Get Account Details API**: Retrieve specific account information, such as balance and transaction history, linked to a session.
13. **Fetch Analytics API**: Retrieve detailed analytics data associated with a specific analytic ID.

## <span style="color: #e74c3c;">Response Status Codes</span>

All API responses are communicated via HTTP using the following status codes:

- **200: OK** – Successful request.
- **201: Created** – New resource created.
- **400: Bad Request** – Invalid request, often due to missing parameters.
- **401: Unauthorized** – No valid API key provided.
- **403: Forbidden** – Insufficient permissions.
- **500: Server Errors** – Issue on Unaport.ai's server.

<div class="line"></div>

## <span style="color: #2ecc71;">Postman</span>

Get started faster with our Postman collection. Click the button below to download.<br><br>
<a href="https://sandbox-fiu-public-docs.s3.ap-south-1.amazonaws.com/PostmanCollections/Unaport.ai+Postman+Collection.postman_collection.json" class="download-button" download>
    <span style="color: #fff; background-color: #3498db; padding: 8px 16px; border-radius: 5px; text-decoration: none;">⬇️ Download Postman Collection</span>
</a>

<div class="line"></div>


### Login API

All the API requests are authenticated using the Bearer token. To get this token, you will need to make a request to the login API using the credentials. The response will contain the token. Send the token in the header for all the requests.

#### Request Table

| Attribute   | Description                | Length | Datatype | Mandatory/Optional | 
|-------------|----------------------------|--------|----------|---------------------|
| `emailId`   | User's email address       | 254    | String   | Mandatory          |
| `password`  | User's password for login  | 8-64   | String   | Mandatory          |

#### Response Table

| Attribute            | Description                                            | Type   |
|----------------------|--------------------------------------------------------|--------|
| `access_token`       | Access token for authenticated user                    | String |
| `expires_in`         | Duration (in seconds) before the access token expires  | Number |
| `refresh_expires_in` | Duration (in seconds) before the refresh token expires | Number |
| `refresh_token`      | Token to obtain a new access token                     | String |
| `token_type`         | Type of token issued, usually "Bearer"                 | String |
| `not-before-policy`  | Timestamp for the policy enforced by the token         | Number |
| `session_state`      | Unique ID for the session state                        | String |
| `scope`              | Authorized scope of access for the user                | String |
| `firstName`          | First name of the user (if available)                  | String |
| `lastName`           | Last name of the user (if available)                   | String |
| `emailId`            | Email ID of the authenticated user                     | String |

### Refresh Token API 

Allows users to obtain a new access token by providing a valid refresh token. This ensures continued access to secured resources without requiring the user to re-authenticate, enhancing user experience and maintaining session continuity.

### Request Table


| Attribute       | Description                      | Length | Datatype | Mandatory/Optional |
|-----------------|----------------------------------|--------|----------|---------------------|
| `refresh_token` | The refresh token for renewing access | 255    | String   | Mandatory          |

### Response Table

| Attribute            | Description                                            | Type   |
|----------------------|--------------------------------------------------------|--------|
| `access_token`       | New access token for the user                          | String |
| `expires_in`         | Duration (in seconds) before the new access token expires | Number |
| `refresh_expires_in` | Duration (in seconds) before the refresh token expires | Number |
| `refresh_token`      | New refresh token                                      | String |
| `token_type`         | Type of token issued, usually "Bearer"                 | String |
| `not-before-policy`  | Timestamp for the policy enforced by the token         | Number |
| `session_state`      | Unique ID for the session state                        | String |
| `scope`              | Authorized scope of access for the user                | String |
| `firstName`          | First name of the user (if available)                  | String |
| `lastName`           | Last name of the user (if available)                   | String |
| `emailId`            | Email ID of the authenticated user                     | String |

### Get Organisation Details API

The API retrieves information about a specific organization using its unique identifier. It provides essential details such as the organization's name, type, and contact information, enabling users to access relevant organizational data

### Request Table

- **URL:** `https://common.sandbox.unaport.com/api/v1/FIU/getOrganisation`
- **HTTP Method:** `GET` 
- **Headers:**
  - **Authorization:** Bearer token for authenticating the request.
  - **Content-Type:** Specifies the request body format (JSON).

### Response Table

| Attribute                            | Description                                                                                     | Type    |
|--------------------------------------|-------------------------------------------------------------------------------------------------|---------|
| `data.id`                            | Unique identifier for the consent record                                                         | String  |
| `data.fiuId`                         | Unique identifier for the Financial Information User (FIU)                                        | String  |
| `data.fiuLive`                       | Live status of the FIU (currently `null`)                                                         | Null    |
| `data.registeredEmail`               | Registered email address of the FIU (currently `null`)                                            | Null    |
| `data.contactNumber`                 | Contact number of the FIU (currently `null`)                                                      | Null    |
| `data.businessPAN`                   | PAN number associated with the business (currently `null`)                                        | Null    |
| `data.nameAsPerPAN`                  | Business name as per PAN (currently `null`)                                                       | Null    |
| `data.pan`                            | PAN number (currently `null`)                                                                     | Null    |
| `data.businessName`                  | Name of the business (currently `null`)                                                           | Null    |
| `data.businessType`                  | Type of business (currently `null`)                                                               | Null    |
| `data.businessModel`                 | Business model (currently `null`)                                                                 | Null    |
| `data.businessDescription`           | Description of the business (currently `null`)                                                    | Null    |
| `data.purposeOfUsingAccountAggregator`| Purpose of using an Account Aggregator (currently `null`)                                         | Null    |
| `data.certificateOfRegistrationFIU`  | Certificate of registration for FIU (currently `null`)                                           | Null    |
| `data.llpinCIN`                      | LL Pin or CIN details (currently `null`)                                                          | Null    |
| `data.gstin`                         | GSTIN details (currently `null`)                                                                  | Null    |
| `data.gstinNumber`                   | GSTIN number (currently `null`)                                                                   | Null    |
| `data.gst`                            | GST information (currently `null`)                                                                | Null    |
| `data.businessAddress`               | Business address (currently `null`)                                                               | Null    |
| `data.city`                           | City of the business (currently `null`)                                                           | Null    |
| `data.pinCode`                        | Pin code of the business (currently `null`)                                                      | Null    |
| `data.state`                          | State where the business is located (currently `null`)                                            | Null    |
| `data.country`                        | Country where the business is located (currently `null`)                                          | Null    |
| `data.businessRegisteredName`        | Registered business name (currently `null`)                                                      | Null    |
| `data.accountNumber`                 | Account number (currently `null`)                                                                 | Null    |
| `data.ifscCode`                      | IFSC code of the business account (currently `null`)                                              | Null    |
| `data.cancelledCheque`               | Cancelled cheque details (currently `null`)                                                       | Null    |
| `data.participationTerms`            | Participation terms (currently `null`)                                                            | Null    |
| `data.fiuAAAgreement`                | Agreement details for the FIU (currently `null`)                                                  | Null    |
| `data.operation`                     | Status of the operation, `0` indicates no operation or pending state                             | Integer |
| `data.status`                        | Status of the consent process (e.g., `PENDING`)                                                  | String  |
| `data.annualTurnoverAccordingToGST`  | Annual turnover according to GST (currently `0`)                                                  | Integer |
| `data.createdAt`                     | Creation timestamp (currently `null`)                                                             | Null    |
| `data.contactDetailsCompleted`       | Indicates whether contact details are completed (`false` in this case)                            | Boolean |
| `data.pancompleted`                  | Indicates whether PAN details are completed (`false` in this case)                               | Boolean |
| `data.businessDetailsCompleted`      | Indicates whether business details are completed (`false` in this case)                           | Boolean |
| `data.gstcompleted`                  | Indicates whether GST details are completed (`false` in this case)                               | Boolean |
| `data.gstbussiness`                  | Indicates whether GST business is completed (`false` in this case)                               | Boolean |
| `fiulive`                            | Current live status of FIU (currently `null`)                                                    | Null    |
| `fiutest.id`                         | ID of the FIU (same as `fiuId`)                                                                   | String  |
| `fiutest.fiuId`                      | FIU ID                                                                                             | String  |
| `fiutest.fiuName`                    | Name of the FIU                                                                                  | String  |
| `fiutest.fiuLogUrl`                  | URL for FIU documentation logs                                                                    | String  |
| `fiutest.version`                    | Version of the FIU                                                                                 | String  |
| `fiutest.fiuStatus`                  | Status of the FIU (e.g., `ACTIVE`)                                                                | String  |
| `fiutest.contactPersonName`          | Name of the contact person for the FIU                                                           | String  |
| `fiutest.contactPersonNumber`        | Contact number of the FIU contact person                                                          | String  |
| `fiutest.contactPersonEmail`         | Contact email of the FIU contact person                                                           | String  |
| `fiutest.assigned`                   | Whether the FIU is assigned (`false` in this case)                                                | Boolean |
| `fiutest.baseUrl`                    | Base URL for FIU API calls                                                                        | String  |
| `fiutest.secretkey`                  | FIU secret key (currently `null`)                                                                  | Null    |
| `fiutest.redirectUrl`                | Redirect URL for consent process                                                                  | String  |
| `fiutest.billingPlan.id`             | ID for the FIU's billing plan                                                                     | String  |
| `fiutest.billingPlan.planName`       | Name of the billing plan (e.g., `Basic Plan`)                                                     | String  |
| `status`                             | Overall status of the API response (`success` in this case)                                       | String  |

<div class="line"></div>


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


### Response Table

| Attribute    | Description                                  | Type    |
|--------------|----------------------------------------------|---------|
| `productId`  | Unique identifier for the inserted product   | String  |
| `status`     | Status of the API operation, e.g., `SUCCESS` | String  |

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

| Attribute       | Description                                                                 | Type    |
|-----------------|-----------------------------------------------------------------------------|---------|
| `ver`           | Version of the consent API response                                        | String  |
| `timestamp`     | Timestamp of when the consent response was generated                        | String  |
| `txnid`         | Transaction ID associated with the consent request                         | String  |
| `Customer.id`   | Unique identifier of the customer, usually in a virtual ID format (VUA)    | String  |
| `ConsentHandle` | Unique handle ID representing the consent                                  | String  |
| `success`       | Message indicating successful creation of the consent                      | String  |
| `redirectUrl`   | URL to redirect the user to complete or view the consent                   | String  |

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

| **Attribute**      | **Description**                                                      | **Type**      |
|--------------------|----------------------------------------------------------------------|---------------|
| `ver`              | The version of the response.                                          | String        |
| `timestamp`        | The timestamp of the response.                                        | String (ISO 8601) |
| `txnid`            | Unique transaction ID for tracking the consent process.               | String        |
| `Customer.id`      | The unique ID of the customer who provided consent.                  | String        |
| `ConsentHandle`    | Unique handle for the created consent.                               | String        |
| `success`          | A message indicating the status of the consent creation.             | String        |
| `redirectUrl`      | URL for redirect after consent is successfully created.              | String        |

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

<div class="line"></div>

### Data Reports

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

### Generate Analytics API

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
| `reportId`          | Unique identifier for the analytics report.               | String (UUID)  |
| `status`            | HTTP status code indicating the success of the request.   | String         |

