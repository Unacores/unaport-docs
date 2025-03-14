<!-- # FIU - Integration with Unaport FIU

## This document provides details for an FIU web SDK to integrate with the Account Aggregator framework via the Unaport FIU solution.

## Introduction

Ink is an RBI-licensed account aggregator, transforming the way individuals and businesses manage their financial data in India. As Ink AA, we offer a secure and streamlined method to consolidate all your financial information in one place. Our service ensures that your data is always accessible, enabling you to manage your finances more efficiently.

Unaport FIU collaborates with Ink to provide comprehensive financial information and insights. With Unaport FIU's cutting-edge technology and Ink's user-friendly interface, you gain a powerful tool that empowers you to make informed financial decisions. Together, Ink and Unaport FIU are transforming financial management in India.

## Web endpoint

Endpoint: [https://websdk.sandbox.unaport.com/unaport](https://websdk.sandbox.unaport.com/unaport)

## SDK config:

<table>
  <tr>
   <td><strong>Field</strong>
   </td>
   <td><strong>Mandatory (M)  \
Optional (O)</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>mobileNumber
   </td>
   <td>M
   </td>
   <td>String
   </td>
   <td>Mobile number of the individual whose data needs to be fetched. Without international code. 10 digits.
   </td>
  </tr>
  <tr>
   <td>fiuName
   </td>
   <td>M
   </td>
   <td>String
   </td>
   <td>Name of the FIU. As per records in Sahamati
   </td>
  </tr>
  <tr>
   <td>logoUrl
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Logo URL to be displayed in the FIU web screens
   </td>
  </tr>
  <tr>
   <td>clientId
   </td>
   <td>M
   </td>
   <td>String
   </td>
   <td>Client ID for Auth
   </td>
  </tr>
  <tr>
   <td>clientSecret
   </td>
   <td>M
   </td>
   <td>String
   </td>
   <td>Client Secret for Auth
   </td>
  </tr>
  <tr>
   <td>callbackUrl
   </td>
   <td>M
   </td>
   <td>String
   </td>
   <td>Url to redirect back to when user exits the Unaport web sdk
   </td>
  </tr>
  <tr>
   <td>colorConfiguration
   </td>
   <td>O
   </td>
   <td>Object
   </td>
   <td>Color Configuration to customize the web screens
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.primaryColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Primary color in Hex color code format.
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.secondaryColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Primary color in Hex color code format.
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.hintColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Hint Color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.borderColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Border color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.primaryButtonColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Primary Button Color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.secondaryButtonColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Secondary Button Color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.disableIconColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Disable icon color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.primaryBackgroundColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Primary background color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.secondaryBackgroundColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Secondary background color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.errorColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Error Color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.errorColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Header Color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.primaryTextColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Primary Text Color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.secondaryTextColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Secondary text color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.invertTextColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Invert Text color
   </td>
  </tr>
  <tr>
   <td>colorConfiguration.failureColor
   </td>
   <td>O
   </td>
   <td>String
   </td>
   <td>Failure Color
   </td>
  </tr>
</table>

### Sample config JSON(plain):

```
{
    "mobileNumber": "9867****13",
    "fiuName": "Unacores FIU UAT",
    "logoUrl": "https://link.to/yourpage/something.png",
    "clientId": "siddhar****tty@hi2.in",
    "clientSecret": "12F&*UFJKD****",
    "callbackUrl": "https://google.com",
    "colorConfiguration": {
        "primaryColor":"#FF23DD",
        "secondaryColor":"#FF23DD",
        "hintColor":"#FF23DD",
        "borderColor":"",
        "primaryButtonColor":"#FF23DD",
        "secondaryButtonColor":"#FF23DD",
        "disableIconColor":"#FF23DD",
        "primaryBackgroundColor":"#FF23DD",
        "secondaryBackgroundColor":"#FF23DD",
        "errorColor":"#FF23DD",
        "headerColor":"#FF23DD",
        "primaryTextColor":"#FF23DD",
        "secondaryTextColor":"#FF23DD",
        "invertTextColor":"#FF23DD",
        "failureColor":"#FF23DD"
    }
}
```

### Sample config Encrypted:

```
2fo88dljax/Jj8bti9Yysyd5VvGm3SrTOADl9baEo2cPRirm0mCH5bGRiR0rFUE5CePPIDeEXTQdwUueDot490Ke0PihySVEACnSafl0bCxJwhMqukipeGTa9psFm9J6N6g70mcAGX0deDGdSRqZsc7C+3CtQ/uww7HzdW/XADrt1gFjhyR+sRH/mtz2sneiIFRkXhxRRD9bwUGNRBKYq+QNxncBz8WsKt+k2XNutMhKmvwEAxYER0u230gVvBBT3cBKVYwmYTWzes9SVhFMHG42hmUY5HPZr/5SMAvBNmLrTELswH51Ea5n8kK2piUAZrk3TKRPje1xNNKDTQnqNM8sUqgvXnCregZSROdkIsfQeGWMmbwfZWZAwr0Hd7W/e80INmYxs/TRiksDSpgHtHF+mJYFm2XzekZY7yrQP+xg6Kz+CUEQNYK1+l7/MG2NPaQM16rL6tYY1OXi57YlftYQMO7j8hIjVV3h7jcEUe47CwsLvCE3o4R+bnm+MRiUf0oF9r8xx2bSNcW6qxcIymMt6fPr8adAjxk6wPCbCTonZdLy4R0RCYsjjEZlRKNy1hAw7uPyEiNVXeHuNwRR7nPXPaeAA+HzSUe7ZO+jYCSqpYF8TC1om9wW5IbzT0dl1kO0xw7tD0rdLH1OBPEkmAlBtp7agVE/5lRPYZu1CmribImWvG4Hexwrxv6Q0wBvYy3p8+vxp0CPGTrA8JsJOoyZaiiKqU5LTgR0zwCf25tjLenz6/GnQI8ZOsDwmwk6cPsLH4VT/3EjR2+e2Vg9futMQuzAfnURrmfyQramJQDz1OWfZTdxpnhjitFL1FThwCZxBu/SsY1sA8FTKliyHeCsWRGH903S9ty2YY9/UI6zPZTdyFYXFT2jx0HEo4ho3Hp+xVPKksas0+xUudZAdOiWtxvqv9oD+xsAVmEg73R7zQg2ZjGz9NGKSwNKmAe00EWk0bvbf3XYrLnboA7iPewiJgrCmFhrMU0EuyFt736a1OzJof79Fl8w+7BZW7gi
```

## Process flow

<ol>
<li>SDK consumer generates config JSON.</li>
<li>JSON is then encrypted using AES-256-ecb algorithm with key provided by us</li>
<li>SDK Consumer redirects the user to Unaport web view, or Loads the page as an Iframe. URL will be &lt;unaport web endpoint&gt;/unaport?config=&lt;encryptedconfigjson&gt;</li>
<li>Unaport FIU securely generates a unique session, authenticates the user in the background using the client id and client secret</li>
<li>Based on the mobile number passed Unaport will securely load a summary of the Users linked accounts and balances</li>
<li><p>If the user has no linked accounts or wants to add additional accounts, User clicks on the link more accounts button to link. Linking steps are as follows:</p>
<ul>
<li>On clicking linked accounts, the Ink AA screen is securely loaded. An OTP is sent to the user for authentication</li>
<li>Upon Authentication, users can select from a list of all FIP (Financial Information Providers)/ Banks.</li>
<li>AA discovers accounts of the user based on his authenticated mobile number.</li>
<li>User selects account(s) to be linked.</li>
<li>User will receive an OTP from the Bank to link account</li>
<li>Upon successful authentication, the user is shown a consent approval screen. He has to accept consent to his data.</li>
<li>On clicking approve his consent is raised and data is securely fetched.</li>
<li>This only needs to be done once per account.</li>
</ul>
</li>
<li><p>User clicks on a particular account, He is able to see the latest transactions of that account, of any bank within the same application.</p>
</li>
<li>User can click on the Account analysis button to view ML powered analytics of his account, spending categories, income and trends.</li>
<li>On the top right of the home page user will also see a notification icon, Upon clicking user recieves personalized nudges based on the data fetched from AA.</li>
<li>User can exit the view as required</li>
</ol>


## Key Features
- Single view of total balances and transactions across all banks.
- ML powered account anlysis, spend categorization and insights.
- Personalized nudges based on cumilative account data. -->