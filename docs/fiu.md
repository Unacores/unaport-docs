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

# Unaport.ai API 

Welcome to the Unaport.ai API Reference. This guide provides all the information you need to integrate Unaport.ai services into your application, including generating user consent, retrieving user details, and accessing analyzed data and CAM sheets. The Unaport.ai APIs are fully RESTful, and all responses are delivered in JSON format.

<img src="https://unacores.github.io/unaport-docs/images/selection.png" align="center" alt="Dashboard" width="700" />

## Introduction

To start with the integration, follow the below steps :-
### Authentication 

<img src="https://unacores.github.io/unaport-docs/images/Login.png" align="center" alt="Dashboard" width="500" />

1. **Login API**: All the API requests are authenticated using the Bearer token. To get this token, you will need to make a request to the login API using the credentials. The response will contain the token. Send the token in the header for all the requests.
2. The **Refresh Token API** allows users to obtain a new access token by providing a valid refresh token. This ensures continued access to secured resources without requiring the user to re-authenticate, enhancing user experience and maintaining session continuity.
3. The **Get Organisation Details API** retrieves information about a specific organization using its unique identifier. It provides essential details such as the organization's name, type, and contact information, enabling users to access relevant organizational data.

### Consents 
<img src="https://unacores.github.io/unaport-docs/images/Consents.png" align="center" alt="Dashboard" width="400" />

4. The **Create Consent Template API** enables users to create a standardized consent template for data sharing among service providers. By defining parameters such as purpose, data types, and expiration, it streamlines the consent management process, ensuring compliance and clarity in user agreements.
5. The **Get Consent Templates List API** retrieves a collection of available consent templates from the system. This allows users to view, manage, and select predefined templates that can be utilized for data sharing agreements, ensuring consistency and compliance across various interactions.
6. The **Create Consent without Template API** allows users to generate a new consent request independently of predefined templates. This provides flexibility for users to define specific parameters, such as data types and sharing purposes, facilitating customized consent agreements tailored to unique data-sharing scenarios.
7.  The **Create Consent with Template API** allows users to generate a new consent request based on a predefined template. By leveraging existing templates, users can ensure compliance and consistency in consent agreements while easily specifying the relevant data types and sharing purposes for the intended data-sharing scenario.
8. The **Check Consent Status API**  allows users to verify the status and details of a specific consent request using its unique consent handle. This enables users to retrieve information about the consent's validity, scope, and associated data-sharing agreements, ensuring transparency and control over consented data access.

### Data Reports
<img src="https://unacores.github.io/unaport-docs/images/Data.png" align="center" alt="Dashboard" width="300" />


9. The **Fetch Data Status API** enables users to retrieve the current status of data sharing associated with a specific consent handle. This API provides insights into whether the consent is active, the data requested, and any updates on the data-sharing process, ensuring users can monitor and manage their consented data effectively.
10. The **Fetch Data API** allows users to retrieve data associated with a specific session identified by its unique session ID. This API provides access to the relevant information tied to the session, enabling users to track and manage data interactions seamlessly within their established sessions.

### Analytics 

<img src="https://unacores.github.io/unaport-docs/images/analytics.png" align="center" alt="Dashboard" width="300" />

11. The **Generate Analytics API** allows users to create detailed analytical reports based on the activities and data interactions associated with a specific session identified by its session ID. This API provides insights into user behavior, data usage patterns, and overall engagement, helping organizations make informed decisions and optimize their services.
12. The **Get Account Details API** enables users to retrieve specific account information linked to a session identified by its unique session ID. This API provides access to essential account data, such as account balance, transaction history, and user details, facilitating effective account management and oversight within the context of the active session.
13. The **Fetch Analytics API** allows users to retrieve detailed analytics data using a unique analytic ID. This API provides insights into specific metrics or reports associated with the analytic ID, enabling users to analyze performance, trends, and other relevant data points for informed decision-making.


Response Status Code
All our API responses are communicated via HTTP using the following status codes :

- **200: Ok**
  - On successful completion of the request.

- **201: Created**
  - Request is successful and a new resource is created.

- **400: Bad Request**
  - Invalid request that cannot be completed, often due to missing parameters.

- **401: Unauthorized**
  - No valid API key provided.

- **403: Forbidden**
  - The API key doesn't have permissions to perform the request.

- **500: Server Errors**
  - Something went wrong on the Unaport.ai server.


<div class="line"></div>

## Postman 

Get started faster with our Postman collection. Click Postman Collection below to download.<br><br>
<a href="https://sandbox-fiu-public-docs.s3.ap-south-1.amazonaws.com/PostmanCollections/FIU+third+party+integration.postman_collection.json" class="download-button" download>
    <span class="icon">⬇️</span> Postman Collection
</a>

<div class="line"></div>

<!--
### Login API

All the API requests are authenticated using the Bearer token. To get this token, you will need to make a request to the login API using the credentials. The response will contain the token. Send the token in the header for all the requests.

#### Request Table

| Attribute  | Description                   | Type   |
|------------|-------------------------------|--------|
| `emailId`  | User's email address          | String |
| `password` | User's password for login     | String |



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

| Attribute       | Description                     | Type   |
|-----------------|---------------------------------|--------|
| `refresh_token` | The refresh token for renewing access | String |

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

-->