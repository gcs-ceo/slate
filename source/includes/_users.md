# Users

Users are the individuals that have accounts created with Makai.

We use a password-less login system that utilized a users phone number and OTP for login.

## Users Table

Field | Type | Null | Description
--------- | ------- | ----------- | -----------
**(PK) Id** | int | NotNullable | Unique Id of the user.
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

Retrieves all users and can be paginated

### HTTP Request

`GET /users` or `GET /users?page=:page&per=:per`

### Query Parameters

Parameter | Default | Description
------- | ------- | -----------
page | 1 | Which page to display
per | nil | If set, will limit the number of users per page

## Create New User

Creates a new user with the given properties

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

### Request Body Schema

Name | Type | Value
--------- | ----------- | ------------
**firstName** | string | First name of the user
**lastName** | string | Last name of the user
**phoneNumber** | string | Phone number of the user in E.164 format
**email** | string | Email of the user
stripeId | string | The Stripe Id of the user
authAccessCode | string | The Authenticating userAccessCode of the user

Required in **bold**

## Update a User

Updates a User's information with the provided properties

## Update User Status

Updates a User's status

## Confirm User Email

Sets User's email to confirmed

## Confirm User Phone

Sets User's phone number to confirmed

## Select User Authorizations

Retrieves a User's data, along with their roles
