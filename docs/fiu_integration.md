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
