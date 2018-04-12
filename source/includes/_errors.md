# Errors

<aside class="notice">Errors are reported back as `"success": false`</aside>

Pharmetika's API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- improperly formatted
401 | Unauthorized -- Your API key or username/password is incorrect
403 | Forbidden -- The endpoint requested requires elevated permissions
404 | Not Found -- The specified endpoint could not be found
405 | Method Not Allowed -- You tried to access an endpoint with an invalid method (e.g. PUT when it should be POST)
429 | Too Many Requests -- Pharmetika has rate-limited the request velocity
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
