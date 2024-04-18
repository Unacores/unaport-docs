# Integrating a FIU backend with your frontend application

Integrating a Financial Information User backend with your frontend application typically involves connecting your frontend interface with a system that manages financial data or transactions.

Our FIU sandbox environment is continuously hosted and accessible for your convenience.

### Unaport FIU Endpoint

The Unaport FIU API root endpoint `https://api.sandbox.unaport.com/backend/api/v1/`

### Create a consent request
This API is used to create a consent request. 

API to call
`https://api.sandbox.unaport.com/backend/api/v1/FIU/Consents/{orgId}`

Method: `POST`

Below `HTTP` headers need to be set when calling the API

  |  Key          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `content-Type` | `application/json` | API request and response are in JSON format |
  | `Authorization` | `Bearer: eyJraWQiOiJyc2ExIiwiYWxnIjoiUlMyNTYifQ.eyJpc3MiOiJjb29raWVqYXIiLCJhdWQiOiJjb29raWVqYXIiLCJleHAiOjE2NDUwNzMyNTksImp0aSI6InJ6THUzQWFEcjFqbTFHbTlxb0VLcXciLCJpYXQiOjE2MTM1MzcyNTksIm5iZiI6MTYxMzUzNzI1OSwic3ViIjoiZmludnVkZW1vIiwiYXpwIjoiZmludnVkZW1vIiwicm9sZXMiOiJhZG1pbiJ9.kCvdxxxdXi69Z8GudZB6JBfcPW6_aC9kTuAQjFUMVqKKxd_JExcqjbsiDRjWLcvhjrNpQZBSIEmQk3eflTnS7rYn7XT2E-jzqIe9j6aE5SsJfNpDp37r_LQK8PEmnOVHaOUnuHha5Hvw8qkKhOOi9Ck94EV4nm-pjWo0VvNEleGTGa1rAL25NJtjMY2MvTJ6dd3o_HaypnJVDmvCZi2LPv7hoiu8awhfc1PQAINtjA7Q9C8jhNhW9vq426ePA8-u3yOKaBw1Pe73IGJfAJzQEBDf-Jp67iBVrEHjUbAbECUst-kxhXKmkwbpD8R_UDzMyW14ze6cgW1S6XHx2kq0Jw`  | The token to be used when calling the APIs | 

Sample Consent creation Request
``` json
 {
    "vuaId": "9867902913@ink",
    "createdBy": "siddharthshetty@hi2.in",
    "trackingId": "test-m",
    "aaId": "UNACORES-AA-UAT",
    "fiuId": "UNACORES-FIU-UAT",
    "redirectUrl": "https://console.sandbox.unaport.com/admin/consent",
    "fiuBaseUrl": "https://api.sandbox.unaport.com/backend/api/v1",
    "ConsentsRequest": {
        "ver": "1.1.2",
        "timestamp": "2024-03-28T05:04:39.821Z",
        "txnid": "00b6c131-bf74-4296-b489-0febc0136b9f",
        "ConsentDetail": {
            "consentStart": "2024-03-28T00:00:00.000Z",
            "consentExpiry": "2024-04-28T00:00:00.000Z",
            "consentMode": "STORE",
            "fetchType": "ONETIME",
            "consentTypes": [
                "PROFILE",
                "SUMMARY",
                "TRANSACTIONS"
            ],
            "fiTypes": [
                "DEPOSIT"
            ],
            "DataConsumer": {
                "id": "UNACORES-FIU-UAT",
            },
            "Customer": {
                "id": "9867902913@ink"
            },
            "Purpose": {
                "code": "101",
                "refUri": "https://api.rebit.org.in/aa/purpose/101.xml",
                "text": "Wealth management service",
                "Category": {
                    "type": "Personal Finance"
                }
            },
            "FIDataRange": {
                "from": "2022-09-28T00:00:00.000Z",
                "to": "2024-03-28T00:00:00.000Z"
            },
            "DataLife": {
                "unit": "DAY",
                "value": 1
            },
            "Frequency": {
                "unit": "DAY",
                "value": 1
            }
        }
    }
}
```

  |  Field Name          |   Values       |	Description	|
  | ------------- |-------------|-------------|
  | `vuaId` | The customer aa account name which can be alpha numeric | API request and response are in JSON format |
  | `createdBy` | Created By who is logged in and creating the cosent request which can be alpha numeric | API request and response are in JSON format |
  | `trackingId` | The tracking id should be unique identifier of consent request which can be alpha numeric | API request and response are in JSON format |
  | `aaId` | AA entity id which can be alpha numeric | API request and response are in JSON format |
  | `fiuId` | FIU entity id which can be alpha numeric | API request and response are in JSON format |
  | `redirectUrl` | AA login url where consent creater login and approve the consent which can be url | API request and response are in JSON format |
  | `fiuBaseUrl` | FIU backend url which can be url | API request and response are in JSON format |
  | `ver` | Consent request version number | API request and response are in JSON format |
  | `timestamp` | Consent request current timestamp format yyyy-MM-dd'T'HH:mm:ss.SSS'Z'| API request and response are in JSON format |
  | `txnid` | Consent unique id which is UUID | API request and response are in JSON format |    
  | `consentMode`	| Allowed values: `STORE` , `VIEW`, `QUERY` | Specifies whether the consent mode is view only, store or query. |
  | `consentTypes` | Allowed values: `PROFILE`, `TRANSACTIONS`, `SUMMARY` | Specifies the account information that can be fetched with this consent i.e. account profile or summary or transactions | 
  | `fiTypes` | Refer to the ReBIT FITypes for possible values [ReBIT Schema](https://api.rebit.org.in/schema) | This specifies the type of Financial Information that can be fetched with this consent. e.g. Deposit accounts (Savings, Current), recurring deposit, etc. |
  | `Purpose` | Possible values of the Purpose/”code” and Purpose/”text” is given in [ReBIT Purpose Codes](https://api.rebit.org.in/purpose) | The consent purpose or purpose for which data is being fetched. |
  | `fetchType` | Allowed values: `ONETIME` or `PERIODIC` | This specifies if the consent can be used once or multiple times i.e. multiple data request can be done or only once 
  	if `ONETIME` , then data can be fetched once only.
	if `PERIODIC`, this consent can be used for multiple data fetches and will be based on the frequency information. |  
  | `Frequency` | `unit` valid values are HOUR, DAY, MONTH, YEAR `value` needs to be numeric | This specifies the frequency of consent usage i.e. the frequency of data requests that can be done.  This is specified with 2 components i.e `UNIT` and `VALUE` . e.g. if `UNIT` is `HOUR` and value is 4 that means data requests can be done 4 times in a HOUR.|
  | `DataLife` | `unit` valid values are `DAY`, `MONTH`, `YEAR`, `INF`  .  `value` needs to be numeric| This signifies for how long can data be stored. Value of `INF` means forever.|
  
  
!!! note "Calculated values for Fields"
	Since this is a product and some of the values need to be calculated when raising a consent request, hence absolute values cannot be provided. For which we have provided fields that help you to define the necessary information for calculation at runtime. 
	
	Fields such as the `consent expiry`, `consent start date`, `data range` are calculated based on when the consent request is raised.  


  |  Field Name          |   Values       |	Description	|
  | ------------- |-------------|-------------|
  | `ConsentExpiry`	| `unit` valid values are DAY, MONTH, YEAR `value` needs to be numeric 	| Specifies when the consent will expire and is controlled by the two fields `unit` and `value` e.g. If `UNIT` is YEAR and `VALUE` is 5, the consent will expire after 5 years. The consentExpiry field in the consent request will have a date and time of 5 years ahead from the instant that the consent is requested.|
  | `consentStartDays` | This has to be a numeric value . (Value of '0' will be taken as current date for the consent request) | This specifies after how many days the consent will start. This gets calculated  when the consent request is raised. |
  
  |  Field Name          |  | Description	|
  | ------------- |-------------|-------------|
  | `dataRangeStartMonths` 	|	`dataRangeEndMonths` | The datarange field is used to specify the data range of the financial information that will be requested. As part of the consent request the data range should be within the consent start and expiry dates. Both these fields are used in conjunction with each other and specify the data range. 	
  
  Example: `dataRangeStartMonths` if 0 and `dataRangeEndMonths` if 5 is interpreted as the dataRangeStart from currentMonth and until next 5 months in future. 
  
  A data range to get last 6 months historic data plus for the next 12 months in the future values can be as below   
  `dataRangeStartMonths` = 6 and `dataRangeEndMonths` = 12  	

Sample Response
``` json
{
  "ver": "1.0",
  "timestamp": "2018-12-06T11:39:57.153Z",
  "txnid": "4a4adbbe-29ae-11e8-a8d7-0289437bf331",
  "Customer": {
    "id": "customer_identifier@AA_identifier"
  },
  "ConsentHandle": "39e108fe-9243-11e8-b9f2-0256d88baae8"
  "success": "Consent created successfully"
  "redirectUrl": "https://api.sandbox.unaport.com/backend/api/v1/redirect/dfdESWW23dx"
}
```
### Get Consent using consent handle

This API retrieves the consent details.

API to call
`https://api.sandbox.unaport.com/backend-v2/api/v2/FIU/GetConsent/{consentHandle}`

Method: `GET`
PARAMETERS:
`consentHandle` The consentHandleId when raising a consent Request

Below `HTTP` headers need to be set when calling the API

  |  Key          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `content-Type` | `application/json` | API request and response are in JSON format |
  | `Authorization` | `Bearer: eyJraWQiOiJyc2ExIiwiYWxnIjoiUlMyNTYifQ.eyJpc3MiOiJjb29raWVqYXIiLCJhdWQiOiJjb29raWVqYXIiLCJleHAiOjE2NDUwNzMyNTksImp0aSI6InJ6THUzQWFEcjFqbTFHbTlxb0VLcXciLCJpYXQiOjE2MTM1MzcyNTksIm5iZiI6MTYxMzUzNzI1OSwic3ViIjoiZmludnVkZW1vIiwiYXpwIjoiZmludnVkZW1vIiwicm9sZXMiOiJhZG1pbiJ9.kCvdxxxdXi69Z8GudZB6JBfcPW6_aC9kTuAQjFUMVqKKxd_JExcqjbsiDRjWLcvhjrNpQZBSIEmQk3eflTnS7rYn7XT2E-jzqIe9j6aE5SsJfNpDp37r_LQK8PEmnOVHaOUnuHha5Hvw8qkKhOOi9Ck94EV4nm-pjWo0VvNEleGTGa1rAL25NJtjMY2MvTJ6dd3o_HaypnJVDmvCZi2LPv7hoiu8awhfc1PQAINtjA7Q9C8jhNhW9vq426ePA8-u3yOKaBw1Pe73IGJfAJzQEBDf-Jp67iBVrEHjUbAbECUst-kxhXKmkwbpD8R_UDzMyW14ze6cgW1S6XHx2kq0Jw`  | The token to be used when calling the APIs | 

Sample Response
``` json
{
    "Data": [
        {
            "id": 1122,
            "trackingId": "0021",
            "vuaId": "8655721266@ink",
            "orgId": "4509dd7b-9ebc-4d93-b1bd-0c2ca7025149",
            "consentHandle": "8d0b4a94-39c2-4108-95e9-206cb956c926",
            "approveStatus": "READY",
            "consentStatus": "ACTIVE",
            "fetchType": "ONETIME",
            "consentId": "ef129007-7a9b-4418-ac89-482e18367149",
            "createdAt": "2024-04-18T07:05:23.089+00:00",
            "notificationDate": "2024-04-18T07:05:43.058+00:00",
            "consentStart": "2024-04-18T00:00:00.000+00:00",
            "consentExpried": "2024-05-18T00:00:00.000+00:00",
            "lastRuntime": "2024-04-18T07:05:43.000+00:00",
            "nextRuntime": null,
            "updatedOn": null,
            "createdBy": "siddharthshetty@hi2.in",
            "aaId": "UNACORES-AA-UAT",
            "consentsDetail": "{\"ver\":\"2.0.0\",\"timestamp\":\"2024-04-18T07:05:23.089Z\",\"txnid\":\"b9580a96-bb7e-4b08-8881-da540ccbd27b\",\"ConsentDetail\":{\"consentStart\":\"2024-04-18T00:00:00.000Z\",\"consentExpiry\":\"2024-05-18T00:00:00.000Z\",\"consentMode\":\"STORE\",\"fetchType\":\"ONETIME\",\"consentTypes\":[\"PROFILE\",\"TRANSACTIONS\",\"SUMMARY\"],\"fiTypes\":[\"NPS\"],\"DataConsumer\":{\"id\":\"UNACORES-FIU-UAT\",\"type\":\"FIU\"},\"Customer\":{\"id\":\"8655721266@ink\"},\"Purpose\":{\"code\":\"101\",\"refUri\":\"https://api.rebit.org.in/aa/purpose/101.xml\",\"text\":\"Wealth management service\",\"Category\":{\"type\":\"Personal Finance\"}},\"FIDataRange\":{\"from\":\"2022-10-18T00:00:00.000Z\",\"to\":\"2024-04-18T00:00:00.000Z\"},\"DataLife\":{\"unit\":\"DAY\",\"value\":2},\"Frequency\":{\"unit\":\"DAY\",\"value\":2}}}",
            "consentidCalled": 0,
            "runCounter": 0,
            "consentidError": null
        }
    ]
}
```

### Fetch Data using sessionId

This API retrieves the account details.

API to call
`https://api.sandbox.unaport.com/backend-v2/api/v2/FIU/FifetchDataBySessionId/{sessionId}`

Method: `GET`
PARAMETERS:
`sessionId` The sessionId must be included in the webhook API calls.

Below `HTTP` headers need to be set when calling the API

  |  Key          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `content-Type` | `application/json` | API request and response are in JSON format |
  | `Authorization` | `Bearer: eyJraWQiOiJyc2ExIiwiYWxnIjoiUlMyNTYifQ.eyJpc3MiOiJjb29raWVqYXIiLCJhdWQiOiJjb29raWVqYXIiLCJleHAiOjE2NDUwNzMyNTksImp0aSI6InJ6THUzQWFEcjFqbTFHbTlxb0VLcXciLCJpYXQiOjE2MTM1MzcyNTksIm5iZiI6MTYxMzUzNzI1OSwic3ViIjoiZmludnVkZW1vIiwiYXpwIjoiZmludnVkZW1vIiwicm9sZXMiOiJhZG1pbiJ9.kCvdxxxdXi69Z8GudZB6JBfcPW6_aC9kTuAQjFUMVqKKxd_JExcqjbsiDRjWLcvhjrNpQZBSIEmQk3eflTnS7rYn7XT2E-jzqIe9j6aE5SsJfNpDp37r_LQK8PEmnOVHaOUnuHha5Hvw8qkKhOOi9Ck94EV4nm-pjWo0VvNEleGTGa1rAL25NJtjMY2MvTJ6dd3o_HaypnJVDmvCZi2LPv7hoiu8awhfc1PQAINtjA7Q9C8jhNhW9vq426ePA8-u3yOKaBw1Pe73IGJfAJzQEBDf-Jp67iBVrEHjUbAbECUst-kxhXKmkwbpD8R_UDzMyW14ze6cgW1S6XHx2kq0Jw`  | The token to be used when calling the APIs | 

Sample Response
``` json
{
    "tabs": [
        {
            "name": "DEPOSIT"
        }
    ],
    "DEPOSIT": {
        "summary": [
            {
                "id": null,
                "currentBalance": "101401773.000",
                "orgId": "4509dd7b-9ebc-4d93-b1bd-0c2ca7025149",
                "branch": "41101",
                "status": "ACTIVE",
                "currency": "INR",
                "fip": "IDFC-FIP",
                "accountNumber": "XXXXXXX1046",
                "sessionId": "f8d0f98d-165f-4d28-a134-c0acee4d0992",
                "fetchType": null,
                "exchangeRate": "",
                "consentId": "04586e55-d950-4a11-b7bb-ffee54ca61f7",
                "balanceDate": null,
                "createdAt": "2024-04-18T06:59:24.663+00:00",
                "facility": "OD",
                "ifscCode": "IDFB0041101",
                "microCode": "461751505",
                "openingDate": "2023-08-17",
                "currentOdLimit": "0.00",
                "drawingLimit": "0.00",
                "accountType": "SAVINGS",
                "compoundingFrequency": null,
                "currentValue": null,
                "description": null,
                "interestComputation": null,
                "interestOnMaturity": null,
                "interestPayout": null,
                "interestPeriodicPayoutAmount": null,
                "interestRate": null,
                "maturityAmount": null,
                "maturityDate": null,
                "principalAmount": null,
                "tenureDays": null,
                "tenureMonths": null,
                "tenureYears": null
            }
        ],
        "accountHolder": [
            {
                "id": null,
                "consentId": "04586e55-d950-4a11-b7bb-ffee54ca61f7",
                "orgId": "4509dd7b-9ebc-4d93-b1bd-0c2ca7025149",
                "name": "Ms. Priyanka  Jalan",
                "dob": "1991-08-01",
                "nominee": "NOT-REGISTERED",
                "email": "priyanka.jalan@idfcfirstbank.com",
                "pan": "GGGGG1111Q",
                "address": "AIROLI,,,Mumbai,400001",
                "mobile": "919748783710",
                "fip": "IDFC-FIP",
                "accountNumber": "XXXXXXX1046",
                "sessionId": "f8d0f98d-165f-4d28-a134-c0acee4d0992",
                "fetchType": "deposit",
                "accountType": "SAVINGS",
                "accountHoldertype": "SINGLE",
                "ckycCompliance": "false",
                "createdAt": "2024-04-18T06:59:24.663+00:00"
            }
        ],
        "transactions": [
            {
                "id": null,
                "orgId": "4509dd7b-9ebc-4d93-b1bd-0c2ca7025149",
                "tranTimestamp": "2024-01-16T15:39:30+05:30",
                "sessionId": "f8d0f98d-165f-4d28-a134-c0acee4d0992",
                "narration": "TEST2",
                "amount": "220022.0",
                "consentId": "04586e55-d950-4a11-b7bb-ffee54ca61f7",
                "type": "CREDIT",
                "mode": "OTHERS",
                "currentBalance": "220022.00",
                "txnId": "0",
                "valueDate": null,
                "reference": "0",
                "balance": null,
                "accountNumber": "XXXXXXX1046",
                "transactionDate": null,
                "createdAt": "2024-04-18T06:59:24.663+00:00"
            },
            {
                "id": null,
                "orgId": "4509dd7b-9ebc-4d93-b1bd-0c2ca7025149",
                "tranTimestamp": "2024-01-16T15:39:33+05:30",
                "sessionId": "f8d0f98d-165f-4d28-a134-c0acee4d0992",
                "narration": "TEST1",
                "amount": "1.0E8",
                "consentId": "04586e55-d950-4a11-b7bb-ffee54ca61f7",
                "type": "CREDIT",
                "mode": "OTHERS",
                "currentBalance": "100220022.00",
                "txnId": "0",
                "valueDate": null,
                "reference": "0",
                "balance": null,
                "accountNumber": "XXXXXXX1046",
                "transactionDate": null,
                "createdAt": "2024-04-18T06:59:24.663+00:00"
            },
            {
                "id": null,
                "orgId": "4509dd7b-9ebc-4d93-b1bd-0c2ca7025149",
                "tranTimestamp": "2024-03-31T22:20:45+05:30",
                "sessionId": "f8d0f98d-165f-4d28-a134-c0acee4d0992",
                "narration": "MONTHLY SAVINGS INTEREST CREDIT",
                "amount": "480844.0",
                "consentId": "04586e55-d950-4a11-b7bb-ffee54ca61f7",
                "type": "CREDIT",
                "mode": "OTHERS",
                "currentBalance": "101401773.00",
                "txnId": "0",
                "valueDate": null,
                "reference": "0",
                "balance": null,
                "accountNumber": "XXXXXXX1046",
                "transactionDate": null,
                "createdAt": "2024-04-18T06:59:24.663+00:00"
            }
        ]
    }
}
```









