# Integrating a FIU backend with your frontend application

Integrating a Financial Information User backend with your frontend application typically involves connecting your frontend interface with a system that manages financial data or transactions.

Our FIU sandbox environment is continuously hosted and accessible for your convenience.

### Unaport FIU Endpoint

The Unaport FIU API root endpoint `https://api.sandbox.unaport.com/backend/api/v1/`


Proceed to CREATE A PRODUCT TEMPLATE or USE Below PRE-CREATED TEMPLATES

  |  PRODUCT TEMPLATE          |   CONSENT TYPE       |	Template Description	|
  | ------------- |-------------|-------------|
  | `ONETIME_DEV_TEMPLATE` | `ONETIME` | Template used for One time consent to fetch PROFILE, SUMMARY & TRANSACTIONSget for last 6 months  |
  | `PERIODIC_DEV_TEMPLATE` | `PERIODIC`  | Periodic Template where data request and fetch can be done 100 times a day to fetch PROFILE, SUMMARY & TRANSACTIONS |
 


### Create a Product Template
Whenever a consent request is raised, the consent parameters and information needs to be provided. In order to reduce repetitive work, errors and also give flexibility for different customers or channels, a product template can be created once and be for raising a consent request. This provides ease and flexibility when interaction with the customer and AA. We have provided an API to create a product template. 

#### Step 1. Create a consent template 

API to call : 
`https://api.sandbox.unaport.com/backend/api/v1/FIU/InsertProduct/{orgId}`

Method : `POST`

Below `HTTP` headers need to be set when calling the API

  |  Key          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `content-Type` | `application/json` | API request and response are in JSON format |
  | `Authorization` | `Bearer: eyJraWQiOiJyc2ExIiwiYWxnIjoiUlMyNTYifQ.eyJpc3MiOiJjb29raWVqYXIiLCJhdWQiOiJjb29raWVqYXIiLCJleHAiOjE2NDUwNzMyNTksImp0aSI6InJ6THUzQWFEcjFqbTFHbTlxb0VLcXciLCJpYXQiOjE2MTM1MzcyNTksIm5iZiI6MTYxMzUzNzI1OSwic3ViIjoiZmludnVkZW1vIiwiYXpwIjoiZmludnVkZW1vIiwicm9sZXMiOiJhZG1pbiJ9.kCvdxxxdXi69Z8GudZB6JBfcPW6_aC9kTuAQjFUMVqKKxd_JExcqjbsiDRjWLcvhjrNpQZBSIEmQk3eflTnS7rYn7XT2E-jzqIe9j6aE5SsJfNpDp37r_LQK8PEmnOVHaOUnuHha5Hvw8qkKhOOi9Ck94EV4nm-pjWo0VvNEleGTGa1rAL25NJtjMY2MvTJ6dd3o_HaypnJVDmvCZi2LPv7hoiu8awhfc1PQAINtjA7Q9C8jhNhW9vq426ePA8-u3yOKaBw1Pe73IGJfAJzQEBDf-Jp67iBVrEHjUbAbECUst-kxhXKmkwbpD8R_UDzMyW14ze6cgW1S6XHx2kq0Jw`  | The token to be used when calling the APIs | 
  
  
Sample Template creation Request
``` json
{
    "product_name": "Deposit",
    "ConsentDetail": {
        "consentStart": "2024-04-17T00:00:00.000Z",
        "consentExpiry": "1",
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
            "id": "UNACORES-FIU-UAT"
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
            "from": "-3",
            "to": "-1"
        },
        "DataLife": {
            "unit": "MONTH",
            "value": 1
        },
        "Frequency": {
            "unit": "MONTH",
            "value": 1
        },
        "DataFilter": [
            {
                "type": "TRANSACTIONAMOUNT",
                "operator": ">=",
                "value": "100"
            }
        ]
    }
}
```  

  |  Field Name          |   Values       |	Description	|
  | ------------- |-------------|-------------|
  | `product_name` | The name of the product which can be alpha numeric | API request and response are in JSON format |
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
    "success": "Product created successfully",
    "status":200

}
``` 

### Check status of Consent Request
This API is used to check the status of a previously raised consent request that is awaiting customer approval. 

API to call
`https://fiu.uatdev.ink-aa.in/ConnectHub/FIU/API/V1/ConsentStatus/<consentHandleId>/<custAAId>`

Method: `GET`

PARAMETERS: 

`consentHandleId` The consentHandleId when raising a consent Request

`custAAId` The Customer AA id

Below `HTTP` headers need to be set when calling the API

  |  Key          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `content-Type` | `application/json` | API request and response are in JSON format |
  | `Authorization` | `Bearer: eyJraWQiOiJyc2ExIiwiYWxnIjoiUlMyNTYifQ.eyJpc3MiOiJjb29raWVqYXIiLCJhdWQiOiJjb29raWVqYXIiLCJleHAiOjE2NDUwNzMyNTksImp0aSI6InJ6THUzQWFEcjFqbTFHbTlxb0VLcXciLCJpYXQiOjE2MTM1MzcyNTksIm5iZiI6MTYxMzUzNzI1OSwic3ViIjoiZmludnVkZW1vIiwiYXpwIjoiZmludnVkZW1vIiwicm9sZXMiOiJhZG1pbiJ9.kCvdxxxdXi69Z8GudZB6JBfcPW6_aC9kTuAQjFUMVqKKxd_JExcqjbsiDRjWLcvhjrNpQZBSIEmQk3eflTnS7rYn7XT2E-jzqIe9j6aE5SsJfNpDp37r_LQK8PEmnOVHaOUnuHha5Hvw8qkKhOOi9Ck94EV4nm-pjWo0VvNEleGTGa1rAL25NJtjMY2MvTJ6dd3o_HaypnJVDmvCZi2LPv7hoiu8awhfc1PQAINtjA7Q9C8jhNhW9vq426ePA8-u3yOKaBw1Pe73IGJfAJzQEBDf-Jp67iBVrEHjUbAbECUst-kxhXKmkwbpD8R_UDzMyW14ze6cgW1S6XHx2kq0Jw`  | The token to be used when calling the APIs | 

Sample Response
``` json
 {
    "header": {
        "rid": "5c9d403d-d9c1-4177-b27e-3aca5a660938",
        "ts": "2019-07-15T11:03:44.427+0000",
        "channelId":  "fiu.uatdev"
    },
    "body": {
        "consentStatus": "ACCEPTED",
        "consentId": 117e8942-1605-4b75-b2db-4b8c953abeae
    }
}
```
The `consentStatus` are as below 

  |   consentStatus       |	Description	|
  | ------------- |-------------|
  | PENDING | Status is pending and consentId is not generated at AA side |
  | ACCEPTED | Status is approved and consentId is generated at AA side and available in the response 
  | REJECTED | Status is rejected. User has rejected the consent request. Consent id is not generated at AA side

### Data request
If consent is ACCEPTED then a data request can be made. When the FI DataRquest is called, the request goes to FIRquest of AA then AA sends notification when Data is ready to FIU. In the response it sends sessionId using which data fetch api can be called.

URL to call 
`https://fiu.uatdev.ink-aa.in/ConnectHub/FIU/API/V1/FIRequest`

Method: `POST`

Below `HTTP` headers need to be set when calling the API

  |  Key          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `content-Type` | `application/json` | API request and response are in JSON format |
  | `Authorization` | `Bearer: eyJraWQiOiJyc2ExIiwiYWxnIjoiUlMyNTYifQ.eyJpc3MiOiJjb29raWVqYXIiLCJhdWQiOiJjb29raWVqYXIiLCJleHAiOjE2NDUwNzMyNTksImp0aSI6InJ6THUzQWFEcjFqbTFHbTlxb0VLcXciLCJpYXQiOjE2MTM1MzcyNTksIm5iZiI6MTYxMzUzNzI1OSwic3ViIjoiZmludnVkZW1vIiwiYXpwIjoiZmludnVkZW1vIiwicm9sZXMiOiJhZG1pbiJ9.kCvdxxxdXi69Z8GudZB6JBfcPW6_aC9kTuAQjFUMVqKKxd_JExcqjbsiDRjWLcvhjrNpQZBSIEmQk3eflTnS7rYn7XT2E-jzqIe9j6aE5SsJfNpDp37r_LQK8PEmnOVHaOUnuHha5Hvw8qkKhOOi9Ck94EV4nm-pjWo0VvNEleGTGa1rAL25NJtjMY2MvTJ6dd3o_HaypnJVDmvCZi2LPv7hoiu8awhfc1PQAINtjA7Q9C8jhNhW9vq426ePA8-u3yOKaBw1Pe73IGJfAJzQEBDf-Jp67iBVrEHjUbAbECUst-kxhXKmkwbpD8R_UDzMyW14ze6cgW1S6XHx2kq0Jw`  | The token to be used when calling the APIs | 

Sample Request body
``` json
Request:
{
	
	"header": {
		"rid": "42c06b9f-cc5b-4a53-9119-9ca9d8e9acdb",
		"ts":  "2019-07-15T11:03:44.427+0000",
	          "channelId":  "netbanking"

	},
	
	"body":{
		
		"custId": "customer1@ink-aa",
		"consentId": "117e8942-1605-4b75-b2db-4b8c953abeae",
		"consentHandleId":"6fa1b74b-62b8-48dd-be2d-696b978aaf8f",
 		"dateTimeRangeFrom": "2018-09-30T08:10:45.006+0000",
        "dateTimeRangeTo": "2019-09-30T08:10:45.006+0000"
	}
	
}
```

  |  Field          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `custId` | A valid customer AA id | This is the virtual AA id of the customer e.g. customer1@ink-aa
  | `consentId` | An ACCEPTED consent by the customer | This is the consent Id received when a consent request is ACCEPTED.
  | `dateTimeRangeFrom` | A valid dateTimeFrom | The from data range for which data is requested. This should be within the data range of the consent.
  | `dateTimeRangeTo` | A valid dateTimeFrom | The to data range for which data is requested. This should be within the data range of the consent.

e.g. This can be for 1 month, or 6 months , etc.	

Sample response. This returns a Session id for the request. 
``` json
{
    "header": {
        "rid": "41f44ca2-4b9a-4310-b6a0-eaaa1349bdd6",
        "ts": "2019-07-15T11:08:21.722+0000",
        "channelId":  "fiu.uatdev"
    },
    "body": {
        "ver": "1.0",
        "timestamp": "2019-07-15T11:08:21.404+0000",
        "txnid": "eeddca07-bccb-4808-8b4a-573322223566",
        "consentId": "117e8942-1605-4b75-b2db-4b8c953abeae",
        "sessionId": "eeb30580-3740-42c4-887b-3f08b929be58",
        "consentHandleId": null
    }
}
```

!!! note "The Session id for status"
	The session id is used for checking the status of the data request.

### Check status of Data Request
This API retrieves the status of the previously sent FIDataRequest.

FIStatus api is called to check whether data is ready or not. If data is ready fiRequestStatus is set to READY or else fiRequestStatus is set to PENDING.

When the fiRequestStatus is READY, it means that the AA has sent the data to fiu.uatdev FIU and FIU has stored the data and ready for channel to fetch. The channel can then call the FIFetch API to retrieve the data into channel.


API to call
`https://fiu.uatdev.ink-aa.in/ConnectHub/FIU/API/V1/FIStatus/<consentId>/<sessionId>/<consentHandle>/<custId>`

Method : `GET`

PARAMETERS: 

`consentId` The consentHandleId when raising a consent Request

`sessionId` The sessionId received in the response of the data request 

`consentHandle` The consentHandle received in the response of the consent request 

`custAAId` The Customer AA id (AA handle)

Below `HTTP` headers need to be set when calling the API

  |  Key          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `content-Type` | `application/json` | API request and response are in JSON format |
  | `Authorization` | `Bearer: eyJraWQiOiJyc2ExIiwiYWxnIjoiUlMyNTYifQ.eyJpc3MiOiJjb29raWVqYXIiLCJhdWQiOiJjb29raWVqYXIiLCJleHAiOjE2NDUwNzMyNTksImp0aSI6InJ6THUzQWFEcjFqbTFHbTlxb0VLcXciLCJpYXQiOjE2MTM1MzcyNTksIm5iZiI6MTYxMzUzNzI1OSwic3ViIjoiZmludnVkZW1vIiwiYXpwIjoiZmludnVkZW1vIiwicm9sZXMiOiJhZG1pbiJ9.kCvdxxxdXi69Z8GudZB6JBfcPW6_aC9kTuAQjFUMVqKKxd_JExcqjbsiDRjWLcvhjrNpQZBSIEmQk3eflTnS7rYn7XT2E-jzqIe9j6aE5SsJfNpDp37r_LQK8PEmnOVHaOUnuHha5Hvw8qkKhOOi9Ck94EV4nm-pjWo0VvNEleGTGa1rAL25NJtjMY2MvTJ6dd3o_HaypnJVDmvCZi2LPv7hoiu8awhfc1PQAINtjA7Q9C8jhNhW9vq426ePA8-u3yOKaBw1Pe73IGJfAJzQEBDf-Jp67iBVrEHjUbAbECUst-kxhXKmkwbpD8R_UDzMyW14ze6cgW1S6XHx2kq0Jw`  | The token to be used when calling the APIs | 


Sample Response
``` json
{
    "header": {
        "rid": "7e61e4d8-f9db-488b-848e-331db1c90f16",
        "ts": "2019-07-15T11:10:32.987+0000",
        "channelId":  "netbanking"
    },
    "body": {
        "fiRequestStatus": "PENDING"
    }
}
```

The `fiRequestStatus` are as below 

  |   fiRequestStatus       |	Description	|
  | ------------- |-------------|
  | PENDING | Requested data IS NOT ready to fetch. |
  | READY | Requested data IS ready to fetch 


### Fetch data
This API is used to fetch the data from fiu.uatdev FIU when the call to FIStatus API returns READY in the fiRequestStatus field.

API to call
`https://fiu.uatdev.ink-aa.in/ConnectHub/FIU/API/V1/FIFetch/<custId>/<consentId>/<sessionId>`

e.g. https://fiu.uatdev.ink-aa.in/ConnectHub/FIU/API/V1/FIFetch/customer1@ink-aa/117e8942-1605-4b75-b2db-4b8c953abeae/eeb30580-3740-42c4-887b-3f08b929be58


METHOD: `GET`

Below `HTTP` headers need to be set when calling the API

  |  Key          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `content-Type` | `application/json` | API request and response are in JSON format |
  | `Authorization` | `Bearer: eyJraWQiOiJyc2ExIiwiYWxnIjoiUlMyNTYifQ.eyJpc3MiOiJjb29raWVqYXIiLCJhdWQiOiJjb29raWVqYXIiLCJleHAiOjE2NDUwNzMyNTksImp0aSI6InJ6THUzQWFEcjFqbTFHbTlxb0VLcXciLCJpYXQiOjE2MTM1MzcyNTksIm5iZiI6MTYxMzUzNzI1OSwic3ViIjoiZmludnVkZW1vIiwiYXpwIjoiZmludnVkZW1vIiwicm9sZXMiOiJhZG1pbiJ9.kCvdxxxdXi69Z8GudZB6JBfcPW6_aC9kTuAQjFUMVqKKxd_JExcqjbsiDRjWLcvhjrNpQZBSIEmQk3eflTnS7rYn7XT2E-jzqIe9j6aE5SsJfNpDp37r_LQK8PEmnOVHaOUnuHha5Hvw8qkKhOOi9Ck94EV4nm-pjWo0VvNEleGTGa1rAL25NJtjMY2MvTJ6dd3o_HaypnJVDmvCZi2LPv7hoiu8awhfc1PQAINtjA7Q9C8jhNhW9vq426ePA8-u3yOKaBw1Pe73IGJfAJzQEBDf-Jp67iBVrEHjUbAbECUst-kxhXKmkwbpD8R_UDzMyW14ze6cgW1S6XHx2kq0Jw`  | The token to be used when calling the APIs | 
  

The request parameters

  |  Field          |   Value       |	Description	|
  | ------------- |-------------|-------------|
  | `custId` | A valid customer AA id | This is the virtual AA id of the customer e.g. customer1@ink-aa
  | `consentId` | An ACCEPTED consent by the customer. | This is the consent Id received when a consent request is ACCEPTED.
  | `sessionId` | The sessionId returned for a submitted data request | The session id used to track the data request for a previously submitted data request.

Sample Response of the fetch returns the decrypted data
``` json
Response:
{
    "header": {
        "rid": "b9da6b54-fa90-42eb-8994-ef3d106de01e",
        "ts": "2019-12-23T09:00:47.423+0000",
                 "channelId":  "fiu.uatdev"
},
"body": [
   {
     "fiObjects": [
        {
           "Transactions": {
               "Transaction": [
                   {
                      "type": "DEBIT",
                      "mode": "ATM",
                      "amount": 6036,
                      "currentBalance": "322644.09",
                      "transactionTimestamp": "2019-07-08T00:00:00.000+0000",
                      "valueDate": "2019-07-08T00:00:00.000+0000",
                      "txnId": "2edce6c8-28f3-462d-8a69-12b84337c165",
                      "narration": "ATW-532676XXXXXX3613-S1AWDD47-DELHI'",
              "reference": "REF6857423"
                    },
                    {
                       "type": "CREDIT",
                       "mode": "ATM",
                       "amount": 10500,
                       "currentBalance": "312144.09",
                       "transactionTimestamp": "2019-07-12T00:00:00.000+0000",
                       "valueDate": "2019-07-12T00:00:00.000+0000",
                       "txnId": "e7d0cbe4-f1c3-4972-be28-432474ac9f71",
                       "narration": "CREDIT INTEREST CAPITALISED",
                       "reference": "REF6857423"
                     }
                ],
               "startDate": "2004-04-12T00:00:00.000+0000",
              "endDate": "2004-04-12T00:00:00.000+0000"
        },
                    "type": "DEPOSIT",
                    "maskedAccNumber": "BOB6857423",
                    "linkedAccRef": "REF6857423",
                    "version": "1.1",
                    "Summary": {
                        "type": "SAVINGS",
                        "branch": "Pune",
                        "facility": "CC",
                        "ifscCode": "SBIN0000454",
                        "micrCode": "411002001",
                        "openingDate": "2018-04-01",
                        "currentODLimit": "120045",
                        "drawingLimit": "20000",
                        "Pending": {
                            "amount": 20
                        },
                        "currentBalance": "175614.64",
                        "currency": "INR",
                        "exchgeRate": "",
                        "balanceDateTime": "2004-04-12T18:20:00.000+0000",
                        "status": "ACTIVE"
                    },
                    "schemaLocation": "http://api.rebit.org.in/FISchema/deposit ../FISchema/deposit.xsd",
                    "Profile": {
                        "Holders": {
                            "type": "JOINT",
                            "Holder": {
                                "name": "Customer Name",
                                "dob": "1994-09-24",
                                "mobile": "9834795713",
                                "nominee": "NOT-REGISTERED",
                                "email": "customer1@youremail.in",
                                "pan": "APS444555",
                                "ckycCompliance": "true"
                            }
                        }
                    }
                }
            ],
            "fipId": "BARB0KIMXXX",
            "custId": "customer1@ink-aa",
            "consentId": "654401e2-9db2-4d6e-b23a-129c169dad81",
            "sessionId": "eb9db8e2-3f9a-42c1-ba12-e7cc0fe637d5"
        }
    ]
}
```
