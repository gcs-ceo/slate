# Important Third Part APIs

These are third party API calls that are important to use to get data needed for other API calls.

Further API documentation can be found at the various websites:

[Authenticating.com API docs](https://docs.authenticating.com/?__hstc=201444046.40a6a11c529501e5c7d159f2d47b131b.1673389659895.1673628342811.1674061931119.5&__hssc=201444046.1.1674061931119&__hsfp=3489631221&_ga=2.167165822.1350423012.1674061929-91823172.1674061929#tag/Introduction)

[Phone Validator API docs](https://www.phonevalidator.com/ApiDoc/V3/)

[Stripe API docs](https://stripe.com/docs/api)

## Validate Phone Number via Phone Validator

> The request returns JSON structured like this:

```json
{
    "Phone": "8888675309",
    "Cost": 0.004,
    "SearchDate": "2023-01-20T11:24:53.721125-08:00",
    "StatusCode": "200",
    "StatusMessage": "OK",
    "PhoneFake": null,
    "PhoneBasic": {
        "PhoneNumber": "8888675309",
        "ReportDate": "2023-01-20T11:24:53.721125-08:00",
        "LineType": "TOLL-FREE",
        "PhoneCompany": "null",
        "PhoneLocation": "UNITED STATES",
        "FakeNumber": "NO",
        "FakeNumberReason": "",
        "ErrorCode": "",
        "ErrorDescription": ""
    },
    "PhoneDetail": null
}
```

This endpoint is a third party API that will verify if the number is valid and the line type.

<aside class="warning">VoIP, Landline, Toll-Free, Unknown, or Fake are not allowed line types</aside>

### HTTP Request

`GET https://api.phonevalidator.com/api/v3/phonesearch?apikey={PHONE_VALIDATOR_API_KEY}&phone={PHONE}&type=basic`

### URL Parameters

Parameter | Description
--------- | -----------
apikey | The Phone Validator Api key
phone | The phone number of the user in E.164 format
type | This type will stay "basic"

## Create User via Authenticating

>Format of the request body:

```json
{
    "firstName": "John",
    "middleName": "Tibba",
    "lastName": "Doe",
    "dob": "22-05-1990",
    "email": "john@doe.com",
    "phone": "+18888675309",
    "houseNumber": ,
    "streetName": "",
    "address": "",
    "city": "",
    "state": "",
    "zipCode": ,
    "ssn": ""
}
```

>Return JSON structured like this:

```json
{
    "userAccessCode": "2237b91d-7bd7-4180-892d-66fb5bed92fd"
}
```

This will create a new user with the provided properties

### HTTP Request

`POST https://api-v3.authenticating.com/user/create`

`Authorization: Bearer {AUTHENTICATING_API_KEY}`

### Request Body Schema

Name | Type | Value
--------- | ----------- | ------------
**firstName** | string | First name of the user
middleName | string | Middle name of the user
**lastName** | string | Last name of the user
**dob** | string | DD-MM-YYYY Date of birth of the user
**email** | string | Email address of the user
**phone** | string | Phone number of the user in E.164 format
houseNumber | int | House Number of the user
streetName | string | Street name of the user
address | string | Address of the user
city | string | City of the user
state | string | State of the user
zipCode | int | Zipcode of the user
ssn | string | Social Security Number of the user

Required in **bold**


## Submit User Consent Via Authenticating

>Format of the request body:

```json
{
    "userAccessCode": "2237b91d-7bd7-4180-892d-66fb5bed92fd",
    "isBackgroundDisclosureAccepted": 1,
    "GLBPurposeAndDPPAPurpose": 1,
    "FCRAPurpose": 1,
    "fullName": "John Tibba Doe"
}
```

> Return JSON structured like this:

```json
{
    "success": true
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`POST https://api-v3.authenticating.com/user/consent`

### Request Body Schema

Name | Type | Value
--------- | ----------- | ------------
**userAccessCode** | string | userAccessCode assigned to user
**isBackgroundDisclosureAccepted** | bool | Instance that background check is needed
**GLBPurposeAndDPPAPurpose** | bool | Certiies intended use permitted by GLBA or DPPA
**FCRAPurpose** | bool | Use of data won't be used for as a factor for any purpose under FCRA
**fullName** | string | Full name of the user

Required in **bold**