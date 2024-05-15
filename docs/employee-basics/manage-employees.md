---
sidebar_position: 1
---

# Manage employees

By leveraging the Numbrs API, you can have one source of truth for your employee data and build integrations that keep data in sync with your HRIS system.

The `employee` endpoint provides a set of API calls that can be used to create, update, and delete employees and their personal information. It's a key part of the Numbrs API, because many other endpoints that are used to manage employee data like contracts, schedules, and more are tied to this endpoint.

## Requirements

- Your integration is [ready to make API calls](https://developer.nmbrs.com/docs#XLYdw)
- You subscribed to the product that API calls are made to from the [Numbrs Developer Portal](https://developer.nmbrs.com/)
- All requests are properly [authenticated](https://nmbrs.stoplight.io/docs/nmbrs-restapi/e9e0f5292b4a1-authentication)
- A company where to add the newly created employees [already exists in the system](https://nmbrs.stoplight.io/docs/nmbrs-restapi/5fad7a8461a01-get-company-list)

## Create employee

Creating an employee is the first step to be able to handle their data. You can create one by making a POST request to the `employee` endpoint. 

```
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

- **COMPANY_ID** is the ID of the company that you're creating an employee in. For example, `ad3562fc-b050-4de7-9eb0-1751eefa680c
`. For more information, see [companies](https://nmbrs.stoplight.io/docs/nmbrs-restapi/5fad7a8461a01-get-company-list).
- BEARER_TOKEN is the bearer token generated from the authentication. For example, `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.
- SUBSCRIPTION_KEY is the subscription key that you generated when you subscribed to the product. For example, `69641f4e3906497da60bee40b6751b0a`.

For more information about the content of the `PersonalInfo` object that you can pass in the request body, check the [personal info object documentation](https://nmbrs.stoplight.io/docs/nmbrs-restapi/6a4f20c9f65fd-personal-info-object).

A successful response will return the newly created employee's ID.

```json
{
  "employeeId": "ID-OF-NEWLY-CREATED-EMPLOYEE"
}
```

Where `ID-OF-NEWLY-CREATED-EMPLOYEE` is the ID of the newly created employee. You can use this ID to retrieve and update the employee data, and delete the employee.x

## Update employee personal info

After creating an employee, you can update their personal information by making a PUT request to the `employee` endpoint. You can pass the ID of the employee you want to update as a URL parameter and the employee data to update in the request body. If you need to retrieve the current information of an employee, use the [Get employee](https://nmbrs.stoplight.io/docs/nmbrs-restapi/eea078fe0d752-get-an-employee) method.

```curl
curl --request POST \
  --url BASE_URL/api/companies/COMPANY_ID/employees \
  --header 'Accept: application/json' \
  --header 'Authorization: BEARER_TOKEN' \
  --header 'Content-Type: application/json' \
  --header 'X-Subscription-Key: SUBSCRIPTION_KEY' \
  --data '{
    "PersonalInfo": {
            DATA
        }
    }
```

Where:

- **COMPANY_ID** is the ID of the company that you're creating an employee in. For example, `ad3562fc-b050-4de7-9eb0-1751eefa680c
`. For more information, see [companies](https://nmbrs.stoplight.io/docs/nmbrs-restapi/5fad7a8461a01-get-company-list).
- **BEARER_TOKEN** is the bearer token generated from the authentication. For example, `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.
- **SUBSCRIPTION_KEY** is the subscription key that you generated when you subscribed to the product. For example, `69641f4e3906497da60bee40b6751b0a`.
- **DATA** is the optional user information that you can include in the request body, just as in the [employee creation](#create-employee) step. Fore more info, check the [personal info object documentation](https://nmbrs.stoplight.io/docs/nmbrs-restapi/6a4f20c9f65fd-personal-info-object).

A successful response returns the user's personal info ID. This ID is an internal ID that the system uses to make the employee's personal information unique. However, you don't need to reference this ID because you can retrieve the employee's personal information by using the `employeeId` that you get when you [create an employee](#create-employee).

```json
{
  "personalInfoId": "756bd0de-fc2f-4b7c-b7ba-d3a3f5360a5b"
}
```

## What's next

Now that you learned how to create and manage an employee's personal information, you're ready to use the employee's personal information in your HRIS system and leverage some of its data, such as the `employeeId`, to call other employee-related endpoints. For example:

- [Create an employee contract](https://nmbrs.stoplight.io/docs/nmbrs-restapi/b93680b32cb75-create-employee-contract)
- [Create an employee bank account](https://nmbrs.stoplight.io/docs/nmbrs-restapi/61886d80827f9-create-employee-bank-account)
- [Create an employee salary](https://nmbrs.stoplight.io/docs/nmbrs-restapi/83554c84ea69a-create-employee-salary)
