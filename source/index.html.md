---
title: SmartScreen API Reference

language_tabs:
  - shell


toc_footers:
  - <a href='http://smartscreen.tech'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

SmartScreen API is used to submit background checking requests. The API is built using RESTful endpoints and standard HTTP verbs.

## Steps

* Get API Keys
* Authenticate API
* Retrieve Package Details
* Create Applicant
* List all reports and status codes
* Retrieve reports

## Usage

1. Get API Keys
You can find the API keys in the settings section under API keys tab after you have successfully setup the account.

2. Authenticate API
To successfully call the SmartScreen API, you will need to send the API key in the Request Header in the parameter name "Authorization" to access these API endpoints.

3. Retrieve Package Details
For sending an applicant with package_id you will have to retrieve the List all the packages to get the details of packagepackage_id is to be sent while creating an applicant in the next API call

4. Create Applicant
The first step is the create an applicantTo create an applicant and create reports for the applicant, send the applicant details with the package_id which will generate reports for applicants based on selected package.

5. List all reports and status codes
The second step after creating applicant is to list the reports and report status for any applicant based on applicant_id retrieved while creation in step 1.

6. Retrieve reports
Retrieve All Reports or individual reports from single report resource based on submitted request parameters.

7. Webhooks
Whenever there is an event relevant to the applicant and its report actions, we shall send a POST to the webhook URl which you configure in the dashboard settings.
  * report created
  * report completed
  * report pending
  * report failed
  * report suspended
  * report resumed


8. Pagination
Pagination is enabled for endpoints that return a list of records.There are two parameters that control pagination: page, which specifies the page number to retrieve, and limit, which indicates how many records each page should contain.

9. Testing
You can make test API calls by using your test API key. Test API requests are free and return fake data.You can find the test API in the settings section from the dashboard

10. Conclusion
You can refer to the API refernce below to check the API endpoints and the required data for these endpoints.

##Test Data
Test Applicant data

* first_name : John
* middle_name : Mark
* last_name : Badboy
* email : john@mail.com
* apt : 123 Vincent House
* street: main st
* state : AS
* city : Anycity
* zipcode : 99999

* ssn : 123-45-6789
* DOB : 1990-12-01


# Authentication

> To authorize, use this code:


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: <auth_token>"
  -H "Content-Type: application/json"
```


> Make sure to replace `<auth_token>` with your API key.

SmartScreen uses API keys to allow access to the API. You can register a new SmartScreen API key at our [User portal](http://smartscreen.tech).

SmartScreen expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: <auth_token>`

<aside class="notice">
You must replace  <code>auth_token</code> with your personal API key.
</aside>


# Package

## Get All Packages


```shell
curl "http://52.23.208.7:6034/v1/package"
  -H "Authorization: <auth_token>" 
  -H "Content-Type: application/json"
```


> The above command returns JSON structured like this:

```json
{
  "status": true,
  "packages": [
    {
      "checklist": [
        {
          "price": 0,
          "code": "idver",
          "title": "ID Verification"
        },
        {
          "price": 0,
          "code": "sexof",
          "title": "Sex Offender"
        },
        {
          "price": 0,
          "code": "gstw",
          "title": "Global Sanction & Terrorist Watchlist"
        },
        {
          "price": 0,
          "code": "natcrim",
          "title": "National Criminal"
        },
        {
          "price": 0,
          "code": "currcrimcounty",
          "title": "County Criminal (Current County)"
        }
      ],
      "price": 11,
      "_id": {
        "$oid": "57a216a0f49bd35c9c6f108d"
      },
      "title": "Basic"
    }
  ]
}
```

This endpoint retrieves all packages assigned to the user.

### HTTP Request

`GET http://52.23.208.7:6034/v1/package`

### Query Parameters
No query parameters required

<aside class="notice">
You must replace <code> <auth_token> </code> with your personal API key.
</aside>


# Applicants

## Create a New Applicant


```shell
curl "http://52.23.208.7:6034/v1/applicant"
  -X POST
  -H "Authorization: <auth_token>" 
  -H "Content-Type: application/json"
  -d '{ \ 
   "applicant": { \ 
     "first_name": "string", \ 
     "middle_name": "string", \ 
     "last_name": "string", \ 
     "email": "string", \ 
     "dob": "string", \ 
     "ssn": "string", \ 
     "apt": "string", \
     "city": "string", \ 
     "state": "string", \ 
     "street": "string", \ 
     "zipcode": "string" \ 
   }, \ 
   "package_id": "string", \ 
   "discount_code": "string" \ 
 }'
```

> Example Request : Create Applicant sample request data structure:

```json
{
  "applicant": {
    "first_name": "string",
    "middle_name": "string",
    "last_name": "string",
    "email": "string",
    "dob": "string",
    "ssn": "string",
    "apt": "string",
    "city": "string",
    "state": "string",
    "street": "string",
    "zipcode": "string"
  },
  "package_id": "string",
  "discount_code": "string"
}
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message": "Applicant created successfully",
  "applicant_id": "581b06ddd6cdaa1e005d3472"
}
```

This endpoint saves an applicant with the selected package for an applicant. Find the package_id from the package API response.

<aside class="warning">Create applicant requires all the applicant information required to complete an order. Please refer to required fields table for processing an applicant report.</aside>

### HTTP Request

`POST http://52.23.208.7:6034/v1/applicant`

### POST Parameters

Parameter | Description
--------- | -----------
applicant | The applicant field has all the applicant related information
package_id | The package_id can be found from the Get Package API
discount_code | Send discount_code if you have got one otherwise it will be blank by default


## Get All Applicants


```shell
curl "http://52.23.208.7:6034/v1/applicant"
  -H "Authorization: <auth_token>" 
  -H "Content-Type: application/json"
```


> The above command returns JSON structured like this:

```json
{
  "status": true,
  "applicants": [
    {
      "last_name": "TestRecord",
      "first_name": "Testscenario-113",
      "_id": {
        "$oid": "581b02cad6cdaa1e005d346f"
      },
      "middle_name": "newTestMiddle"
    },
    {
      "last_name": "TestRecord",
      "first_name": "Testscenario-113-2",
      "_id": {
        "$oid": "581b06ddd6cdaa1e005d3472"
      },
      "middle_name": "newTestMiddle"
    }
  ]
}
```

This endpoint retrieves all applicants for the user.

### HTTP Request

`GET http://52.23.208.7:6034/v1/applicant`

### Query Parameters
No query parameters required


# Order

## Create Order


```shell
curl "http://52.23.208.7:6034/v1/order"
  -X POST
  -H "Authorization: <auth_token>" 
  -H "Content-Type: application/json"
```


> The above command returns JSON structured like this:

```json
{
  "status" : true,
  "message" : "Order created successfully",
  "order_id" : "string",
  "applicant_id" : "string"
}
```

This endpoint creates a new order for an applicant.

### HTTP Request

`POST http://52.23.208.7:6034/v1/order`

### POST Parameters
Parameter | Value
--------- | -----------
applicant_id | The Applicant ID for an applicant
package_id | Package Title for the applicant


# Reports

## Report Type

You can send SmartScreen API a report_type parameter to retrieve a specific report for a specific applicant, report_type field may consist any of the following values

### 1. SSN Trace
The SSN Trace happens on the SSN ID of the applicant, send ssn in the applicant creation API to perform SSN Trace

To retrieve SSN Trace report send the following parameters in the Get single report API

### POST Parameters
Parameter | Value
--------- | -----------
report_type | ssntrace
search_id | search_id retrieved from the report status API

### 2. County Criminal 

To retrieve County Criminal report send the following parameters in the Get single report API

### POST Parameters
Parameter | Value
--------- | -----------
report_type | crimcounty
search_id | search_id retrieved from the report status API


### 3. Nationwide Criminal

To retrieve Nationwide Criminal report send the following parameters in the Get single report API

### POST Parameters
Parameter | Value
--------- | -----------
report_type | nationalcrim
search_id | search_id retrieved from the report status API


### 4. Global Sanctions and Terrorist Watchlist

To retrieve Global Sanctions and Terrorist Watchlist report send the following parameters in the Get single report API

### POST Parameters
Parameter | Value
--------- | -----------
report_type | terroristwl
search_id | search_id retrieved from the report status API


### 5. Driving Record

To retrieve Driving Record report send the following parameters in the Get single report API

### POST Parameters
Parameter | Value
--------- | -----------
report_type | drivinglicense
search_id | search_id retrieved from the report status API

### 6. Sex offender

To retrieve Sex offender report send the following parameters in the Get single report API

### POST Parameters
Parameter | Value
--------- | -----------
report_type | sexoff
search_id | search_id retrieved from the report status API


### 7. Employment Verification

To retrieve Employment Verification report send the following parameters in the Get single report API

### POST Parameters
Parameter | Value
--------- | -----------
report_type | employmentverification
search_id | search_id retrieved from the report status API

### 8. Education Verification

To retrieve Driving Record report send the following parameters in the Get single report API

### POST Parameters
Parameter | Value
--------- | -----------
report_type | educationverification
search_id | search_id retrieved from the report status API

### 9. Drug Test

To retrieve Drug Test report send the following parameters in the Get single report API

### POST Parameters
Parameter | Value
--------- | -----------
report_type | drugtest
search_id | search_id retrieved from the report status API



## Get Report Status with search_id


```shell
curl "http://52.23.208.7:6034/v1/report/applicant_id"
  -H "Authorization: <auth_token>" 
  -H "Content-Type: application/json"
```


> The above command returns JSON structured like this:

```json
{
  "status": true,
  "reports": [
    {
      "status": "pending",
      "report_type": "drivinglicense",
      "search_id": "57c83ef6c951f59298c7a8b5"
    },
    {
      "status": "complete",
      "report_type": "nationalcrim",
      "search_id": "57c83ef6c951f59298c7a8b5"
    },
    {
      "status": "pending",
      "report_type": "terroristwl",
      "search_id": "57c83ef6c951f59298c7a8b5"
    },
    {
      "status": "complete",
      "report_type": "ssntrace",
      "search_id": "57c83ef6c951f59298c7a8b5"
    }
  ]
}
```

This endpoint retrieves all Report with status for an applicant.

### HTTP Request

`GET http://52.23.208.7:6034/v1/report/applicant_id`

### URL REST Parameters
Parameter | Description
--------- | -----------
applicant_id | The Applicant ID for an applicant



## Get All Report Result


```shell
curl "http://52.23.208.7:6034/v1/report"
  -H "Authorization: <auth_token>" 
  -H "Content-Type: application/json"
```

> Sample Request Data:

```json
{
  "applicant_id" : "57a2dbb6f49bd351d695ab4e"
}
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "reports": [
    {
      "status": "pending",
      "request": {
        "applicant_id": "58145aa9c951f58e351ecbfc"
      },
      "response": null,
      "report_type": "nationalcrim",
      "status_message": "",
      "search_id": null
    },
    {
      "status": "complete",
      "request": {
        "applicant_id": "58145aa9c951f58e351ecbfc"
      },
      "response": {
      },
      "report_type": "ssntrace",
      "status_message": "",
      "search_id": "57c83ef6c951f59298c7a8b5"
    }
  ]
}
```

This endpoint retrieves all Report with response and statue for an applicant.

### HTTP Request

`GET http://52.23.208.7:6034/v1/report`

### URL REST Parameters
Parameter | Description
--------- | -----------
applicant_id | The Applicant ID for an applicant



## Get Single Report Result


```shell
curl "http://52.23.208.7:6034/v1/report"
  -H "Authorization: <auth_token>" 
  -H "Content-Type: application/json"
```

> Sample Request Data:

```json
{
  "applicant_id" : "57a2dbb6f49bd351d695ab4e",
  "report_type": "ssntrace",
  "search_id": "57c83ef6c951f59298c7a8b5"
}
```

> The above command returns JSON structured like this:

```json
{
  "status": true,
  "report": {
    "status": "complete",
    "request": {
      "applicant_id": "58145aa9c951f58e351ecbfc"
    },
    "response": {
      "ssntrace" : "response"
    },
    "report_type": "ssntrace",
    "status_message": "Report Completed",
    "search_id": "57c83ef6c951f59298c7a8b5"
  }
}
```

This endpoint retrieves a single Report with response and status for an applicant.

### HTTP Request

`GET http://52.23.208.7:6034/v1/report`

### URL REST Parameters
Parameter | Description
--------- | -----------
applicant_id | The Applicant ID for an applicant
report_type | Report Type section mentions the report type
search_id | search_id can be retrieved from the Report Status API

