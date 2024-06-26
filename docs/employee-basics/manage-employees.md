---
sidebar_position: 1
---

# Manage employees

By leveraging the Numbrs API, you can have one source of truth for your employee data and build integrations that keep data in sync with your HRIS system.

The API provides a set of employee-related endpoints and API calls that you can use to create, update, and delete employees and their personal information. Employees are a key part of the Numbrs API, because many other endpoints that are used to manage data like contracts, schedules, and more are tied to an employee.

## Requirements

- Your integration is [ready to make API calls](https://developer.nmbrs.com/docs#XLYdw)
- You subscribed to the product that API calls are made to from the [Numbrs Developer Portal](https://developer.nmbrs.com/)
- All requests are properly [authenticated](https://nmbrs.stoplight.io/docs/nmbrs-restapi/e9e0f5292b4a1-authentication)
- A company where to add the newly created employees [already exists in the system](https://nmbrs.stoplight.io/docs/nmbrs-restapi/5fad7a8461a01-get-company-list)

## Create employee

Creating an employee is the first step to be able to handle their data. You can create one by making a `POST` request to the [`employees` endpoint](https://nmbrs.stoplight.io/docs/nmbrs-restapi/13c6a8d9c7190-create-employee). To create an employee, you need to pass the company ID in the URL parameter.

```curl
curl --request POST \
  --url BASE_URL/api/companies/COMPANY_ID/employees \
  --header 'Accept: application/json' \
  --header 'Authorization: BEARER_TOKEN' \
  --header 'Content-Type: application/json' \
  --header 'X-Subscription-Key: SUBSCRIPTION_KEY' \
  --data '{
  "PersonalInfo": {
    "basicInfo": {
      "employeeNumber": 98072,
      "firstName": "John",
      "firstNameInFull": "string",
      "prefix": "van der",
      "initials": "string",
      "lastName": "Doe",
      "employeeType": "applicant"
    },
    "birthInfo": {
      "birthDate": "1980-02-27",
      "birthCountryCodeISO": "NL",
      "nationalityCodeISO": "PT",
      "deceasedOn": "1980-02-27",
      "gender": "unspecified"
    },
    "contactInfo": {
      "privateEmail": "doe@private.com",
      "businessEmail": "doe@business.com",
      "businessPhone": "+351222222",
      "businessMobilePhone": "+351222222",
      "privatePhone": "+351222222",
      "privateMobilePhone": "+351222222",
      "otherPhone": "+351222222"
    },
    "partnerInfo": {
      "partnerPrefix": "string",
      "partnerName": "string",
      "ascriptionCode": 0
    },
    "period": {
      "year": 2021,
      "period": 4
    },
    "createdAt": "2021-07-01T10:15:08Z"
  },
  "AdditionalEmployeeInfo": {
    "inServiceDate": "2019-08-24",
    "defaultEmployeeTemplate": "string"
  }
}'
```

Where:

- **BASE_URL** is the base URL of the Numbrs API. For example, `https://api.nmbrs.com`.
- **COMPANY_ID** is the unique ID of the company that you're creating an employee in. For example, `ad3562fc-b050-4de7-9eb0-1751eefa680c`. For more information, see [companies](https://nmbrs.stoplight.io/docs/nmbrs-restapi/5fad7a8461a01-get-company-list).
- **BEARER_TOKEN** is the bearer token generated from the authentication. For example, `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.
- **SUBSCRIPTION_KEY** is the subscription key that you generated when you subscribed to the product. For example, `69641f4e3906497da60bee40b6751b0a`.

:::tip
For more information about the content of the `PersonalInfo` object that you can pass in the request body, check the [personal info object documentation](https://nmbrs.stoplight.io/docs/nmbrs-restapi/6a4f20c9f65fd-personal-info-object).
:::

A successful response will return the newly created employee's ID.

```json
{
  "employeeId": "ID-OF-NEWLY-CREATED-EMPLOYEE"
}
```

Where `ID-OF-NEWLY-CREATED-EMPLOYEE` is the unique ID of the newly created employee. You can use this ID to retrieve and update the employee data, and delete the employee.

## Update employee personal info

After creating an employee, you can update their personal information by making a `PUT` request to the [`personalInfo` endpoint](https://nmbrs.stoplight.io/docs/nmbrs-restapi/e12e45d11695c-update-employee-personal-info). You can pass the unique ID of the employee you want to update as a URL parameter and the employee information to update in the request body.

:::tip RETRIEVE USER INFO
If you need to retreieve the employee's personal information before you update it, you can send a `GET` request to the [`employeeId` endpoint](https://nmbrs.stoplight.io/docs/nmbrs-restapi/eea078fe0d752-get-an-employee).
:::

```curl
curl --request PUT \
  --url BASE_URL/api/employees/EMPLOYEE_ID/personalInfo \
  --header 'Accept: application/json' \
  --header 'Authorization: BEARER_TOKEN' \
  --header 'Content-Type: application/json' \
  --header 'X-Subscription-Key: SUBSCRIPTION_KEY' \
  --data '{
      DATA
    }'
```

Where:

- **BASE_URL** is the base URL of the Numbrs API. For example, `https://api.nmbrs.com`.
- **EMPLOYEE_ID** is the unique ID of the employee that you want to update. For example, `ad3562fc-b050-4de7-9eb0-1751eefa680c`. This ID is generated when you create the employee, but you can also retrieve it by using the [`employee list` endpoint](https://nmbrs.stoplight.io/docs/nmbrs-restapi/a31578b069764-get-employee-list).
- **BEARER_TOKEN** is the bearer token generated from the authentication. For example, `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.
- **SUBSCRIPTION_KEY** is the subscription key that you generated when you subscribed to the product. For example, `69641f4e3906497da60bee40b6751b0a`.
- **DATA** is the optional user information that you can include in the request body, just as in the [employee creation](#create-employee) step. Fore more information, check the [personal info object documentation](https://nmbrs.stoplight.io/docs/nmbrs-restapi/6a4f20c9f65fd-personal-info-object).

A successful response returns the user's personal info ID.

```json
{
  "personalInfoId": "756bd0de-fc2f-4b7c-b7ba-d3a3f5360a5b"
}
```

:::info
`personalInfoId` is an internal ID that we use to make the employee's personal information unique. You don't need to reference this ID because you can retrieve the employee's personal information by using the `employeeId` that you get when you [create an employee](#create-employee).
:::

## What's next

Now that you learned how to create and manage an employee's personal information, you're ready to use the employee's personal information in your HRIS system and leverage some of its data, such as the `employeeId`, to call other employee-related endpoints. For example:

- [Create an employee contract](https://nmbrs.stoplight.io/docs/nmbrs-restapi/b93680b32cb75-create-employee-contract)
- [Create an employee bank account](https://nmbrs.stoplight.io/docs/nmbrs-restapi/61886d80827f9-create-employee-bank-account)
- [Create an employee salary](https://nmbrs.stoplight.io/docs/nmbrs-restapi/83554c84ea69a-create-employee-salary)
