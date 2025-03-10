# FIU - Integration with Unaport FIU

## Overview

Unaport provides a Web SDK designed for seamless integration with web and mobile applications (via WebView).

This SDK enables FIUs to maintain their own branding and user experience without directly consuming APIs. Users can approve or reject their consent requests within the application rather than through external AA apps.

Currently, the SDK supports Finvu as an Account Aggregator (AA), with plans to add more AAs, including Ink, in future updates.

## SDK Endpoints

- **Sandbox**: [Unaport Sandbox SDK](https://sdk.sandbox.unaport.com/view)
- **Premium**: [Unaport Premium SDK](https://sdk.premium.unaport.com/view)

## Key Features

- **Customizable UI**: Adaptable color scheme to match the FIU brand.
- **Effortless Integration**: Plug-and-play setup with no need for developers to manage process flow.
- **Seamless Consent Management**: Direct consent creation and approval without redirection.

## Process Flow

1. **Encrypt JSON Configuration**: Pass the encrypted JSON in the URL. Follow the [Process for Generating Encrypted SDK Configuration](#process-for-generating-encrypted-sdk-configuration).
2. **Redirect to Unaport Web SDK**: The SDK consumer redirects the user to Unaport's WebView or loads it as an iframe.
    - Example URL: `<unaport-web-endpoint>/view?config=<encryptedconfigjson>`
3. **Select Banks/FIP**:
    - User will select the bank name from the list in the first screen. Based on the Selected FIP they will be able to link their account approve their consent for the selected bank/fips.
    ![Select Banks](images/sdk1.png)
4. **Consent Creation & Authentication**:
    - The SDK securely creates consent using the provided template ID.
    - The user is authenticated in the background.
    - The SDK redirects to the AA OTP screen.
    ![Enter AA OTP](images/sdk2.png)
5. **Linked Account Summary**:
    - Based on the provided mobile number and Selected Bank, Unaport securely retrieves and displays the user's linked accounts and Discovered Accounts if not linked.
    - If no accounts are linked, or additional accounts need to be added, the user can link them via the "Link Button" option:
     - A bank OTP is required for account linking.
     ![Enter Bank OTP](images/sdk3.5.png)
     - Upon successful authentication, the user reviews and approves consent.
     ![Approve Consent](images/sdk4.png)
6. **Exit Option**:
    - Users can exit the view anytime as needed.
    ![Exit](images/sdk5.png)

## Process for Generating Encrypted SDK Configuration

1. Convert the configuration JSON to a Base64-encoded string.
2. Convert the Base64 string to a URL-encoded string.
3. Append the encoded string to the config parameter in the URL.
    - Example:
      ```
      https://<sdk-URL>/view?config={url-encoded-string}
      ```

## SDK Configuration Parameters

| Field                | Required | Type   | Description                                                                            |
| -------------------- | -------- | ------ | -----------------------------------------------------------                            |
| `phoneNumber`        | M        | String | 10-digit mobile number (without country code).                                         |
| `trackingId`         | M        | String | Tracking ID for the New Consent as per your reference                                  |
| `fiuId`              | M        | String | FIU Id as registered in Sahamati.                                                      |
| `accessToken`        | M        | String | Access Token generated from the Login URL                                              |
| `refreshToken`       | M        | String | Refresh Token generated from the Login URL                                             |
| `theme`              | M        | Json   | Customizable UI color settings. Find Config [here](#color-configuration-fields)        |

### Color Configuration Fields
| Field                      | Required | Type   | Description                      |
| -------------------------- | -------- | ------ | -------------------------------- |
| `background`               | M        | String | Background color (Hex code).     |
| `accent`                   | M        | String | Accent color (Hex code).         |
| `primary`                  | M        | String | Primary text color.              |
| `primaryText`              | M        | String | Primary border color.            |
| `primaryButtonText`        | M        | String | Primary button text color.       |
| `secondary`                | M        | String | Secondary button background.     |
| `secondaryText`            | M        | String | Secondary text color.            |
| `disabled`                 | M        | String | Disabled background color.       |
| `disabledText`             | M        | String | Disabled text color.             |
| `border`                   | M        | String | Border color.                    |
| `hintText`                 | M        | String | Hint text color.                 |
| `errorText`                | M        | String | Error message text color.        |
| `loaderColor`              | M        | String | Loader indicator color.          |
| `fontName`                 | M        | String | Font family name.                |
| `failureColor`             | M        | String | Failure state indicator color.   |

## Sample Configuration JSON (Plaintext)

```json
{
  "theme": {
    "background": "#131313",
    "accent": "#1B1B1B",
    "primary": "#7762FF",
    "primaryText": "#FFFFFF",
    "primaryButtonText": "131313",
    "secondary": "#C589E4",
    "secondaryText": "#F2F2F2",
    "disabled": "#1F1F1F",
    "disabledText": "#FEFEFE",
    "border": "#767676",
    "hintText": "#9e9e9e",
    "errorText": "#d32f2f",
    "loaderColor": "#F2F2F2",
    "fontName": "Open Sans"
  },
  "productId": "5961868f-ac0e-45e6-9e7b-394c535fa4cc",
  "phoneNumber": "98******92",
  "trackingId": "Created from Unaport SDK",
  "fiuId": "**Id",
  "accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJ5TVczMnpfZ0stT2NSS3N2MkdsRV9EbFFmTy1JX3psaTVLTW0yMGE1VFFZIn0.eyJleHAiOjE3NDE0MjYwMjYsImlhdCI6MTc0MTQyNTQyN29tIiwiZW1haWwiOiJkZXZlbG9wZXJAdW5hY29yZXMuY29tIn0.gjRucWiTB4Jpe52VENQLVXI5pj7QgsFQqQuoGwDffYi-K_DXbjaqltwPs6pXHo1qLI3uuJT2TZ7YP7-Le3iTGkcqBo5AcH-1asyR-pHwF92nFwfEu3PJdVwC4PP1S1L-U0tEsG4RcdJUO1QHfTgmOE9fj7Ca4TzXQ",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJmZDA4M2JiOC1mOTBlLTRjNTItYWZjZi1iZDQxNzEwNGIwNGQifQ.eyJleHAiOjE3NDE0MjcyMjYsImlhdCI6MTc0MTQyNTQyNiwianRpIjoiNzRmODM0ZjItMTczZS00OWE4LTlmNjQtMWVhZWNmMmY3MGQ1IiwiaXNzIjoiaHR0cHM6Ly9rZXljbG9hay5zYW5kYm94LnVuYXBvcnQuY29tL2F1dGgvcmVhbG1FuZGJveC51bmFwb3J0LmNvbS9hdXRoL3JlYWxtcy9GSswzPN0"
}
```
