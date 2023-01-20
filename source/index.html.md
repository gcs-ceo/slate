---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript
  - csharp

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```javascript
```

```csharp
```

> Make sure to replace `{YOUR_API_KEY}` with your API key.

Makai uses API keys to allow access to the API.

Makai expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: {YOUR_API_KEY}`

<aside class="notice">
You must replace <code>{YOUR_API_KEY}</code> with your personal API key.
</aside>

Makai also uses multiple third party APIs that will be needed to make certain API calls.

<aside class="notice">
These third Pary API Keys should be stored as variables for better protection.
</aside>

# Users

## Users Table

Field | Type | Null | Description
--------- | ------- | ----------- | -----------
**(PK) Id** | int | No | Unique Id of the user.
**Phone** | nvarchar(50) | No | Users Phone number in E.164 format
**Email** | nvarchar(100) | NotNullable | Users email address
FirstName | nvarchar(100) | Nullable | Users first name
LastName | nvarchar(100) | Nullable | Users last name
AvatarUrl | nvarchar(255) | Nullable | Users avatar url
Stripe_Id | nvarchar(100) | Nullable | Users unique Stripe Customer Id
Auth_Code | nvarchar(200) | Nullable | Users uniqie Authenticating userAccessCode
**PhoneConfirmed** | bit | NotNullable | Default 0, Specifies if User has confirmed thier number
**EmailConfirmed** | bit | NotNullable | Default 0, Specifies if User has confirmed thier email
**UserStatusId** | int | NotNullable | Default 1, Id of the status that user currently is
**DateCreated** | datetime2 | NotNullable | Default (getutcdate()) Date the user was created
**DateModified** | datetime2 | NotNullable | Default (getutcdate()) Date the user was last modified

Required in **bold**

## List All Users

This endpoint retrieves all users and can be paginated

### HTTP Request

`GET /users` or `GET /users?page=:page&per=:per`

### Query Parameters

Parameter | Default | Description
------- | ------- | -----------
page | 1 | Which page to display
per | nil | If set, will limit the number of users per page

## Create New User

>Format of the request body:

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "phoneNumber": "+18888675309",
  "email": "john@doe.com",
  "stripeId": "",
  "authAccessCode": "",
}
```

>Return JSON structured like this:

```json
{
  "id": "0001",
  "firstName": "John",
  "lastName": "Doe",
  "phoneNumber": "+18888675309",
  "email": "john@doe.com",
  "stripeId": "cus_NCSqlAx2JjtwQb",
  "authAccessCode": "2237b91d-7bd7-4180-892d-66fb5bed92fd",
  "phoneConfirmed": 0,
  "emailConfirmed": 0,
  "userStatus": 1,
  "userRoles": [
      "user"
    ],
  "dateCreated": "2023-01-01 08:45:36.576",
  "dateModified": "2023-01-01 08:45:36.576"
}
```

This will create a new user with the provided properties

### HTTP Request

`POST /users`

### Query Parameters

None

## Validate Phone Number

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
{PHONE_VALIDATOR_API_KEY} | The Phone Validator Api key
{PHONE} | The phone number of the user in E.164 format

## Create User via Authenticate

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

### Query Parameters

None

## Delete a Specific Kitten

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

```csharp
````

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

