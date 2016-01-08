# Errors

The EoneoPay API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- The request is missing required parameters or the provided parameters are not valid
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The resource requested is hidden for administrators only
404 | Not Found -- The specified resource could not be found
405 | Method Not Allowed -- You tried to access a resource with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The resource requested has been removed from our servers
429 | Too Many Requests -- You're requesting too many resources
500 | Internal Server Error -- An internal server error has occurred. Please report this to the helpdesk.
503 | Service Unavailable -- We're temporarially offline for maintenance. Please try again later.
