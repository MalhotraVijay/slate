# Errors

<aside class="notice">SmartScreen API will send error code when there is an error for the request sent. The response will contain a key errorCode which will be the reason for the occurance of error.</aside>


> The above command returns JSON structured like this:

```json
{
  "status": true,
  "message" : "Error message",
  "error_code" : error_code
}
```

The SmartScreen API uses the following error codes:


Error Code | Meaning
---------- | -------
101 | Report Failed -- The report processing failed
102 | Report Pending -- The report is in pending state
103 | Value Error -- Values sent in the request are not correct
104 | Incomplete applicant information -- The specified Applicant information is either invalid or incomplete
105 | Invalid Billing Option -- Your billing options are incorrect
106 | Unauthorised access -- You are not authorized to make this request
500 | Internal Server Error -- We had a problem with our server. Try again later.
