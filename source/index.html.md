---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - javascript

toc_footers:
  - <a href='https://app.oxalis.cl/users/sign_in'>Sign Up for a Developer Key</a>
  - <div>&#169; 2018 Corporate Legal Solutions</div>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Oxalis2 API! You can use our API to access Oxalis2 API endpoints, which can get information of client's requests in our database.

We have language bindings Shell, Ruby, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Version
Version: 1.0.0

URL: [Oxalis2 API](https://app.oxalis.cl/api/v1/)

# Request credentials

The credentials must be requested to Corporate Legal Solutions

# Authentication

Oxalis2 uses API username and API password to allow access to the API. You can get these at our [Oxalis](http://oxalis.cl).

Oxalis expects for the API username and API password to be included in all API requests to the server in a header that looks like the following:

<aside class="notice">
  You must replace <code>username</code> and <code>password</code>  with your personal API info.
</aside>

# Authenticate
<p class="explanation">
  Add auth parameters in <strong>Header</strong>
</p>

`Header: username` `Header: password`

<p><strong>URL Parameters</strong></p>

Parameter | Type | Example | Description
--------- | ---- | ------- | -----------
username|string|company_username|Identifier to use API resources
password|string|company_password|Password to use API resources

> Make sure to replace `username` and `password` with your API username and API password respectively.

 <aside class="success">
   Remember — a happy user is an authenticated user!
</aside>

# Client's request management
  <p class="explanation">
  This session allows you to manage client's requests
  <span>To better understand, review the examples in different languages</span>
  </p> 

### GET ALL REQUESTS
 <p><span class="label label-info">GET</span>/requests</p>
  <p><strong>URL Parameters</strong></p>
  
  Parameter | Type | Example | Description
  --------- | ---- | ------- | -----------
  
> Example for get all requests

```shell
  curl -X GET "https://app.oxalis.cl/api/v1/requests" \
    -H "username: company_username" \
    -H "password: company_password"
```

```ruby
  require 'rest-client'
  require 'json'
  
 response = RestClient::Request.execute(method: :get,
                                        url: 'http://app.oxalis.cl/api/v1/requests',
                                        headers: { username: 'company_username',
                                                   password: 'company_password'})
 result = JSON.parse(response) 
 result
 
```

```javascript
  // not implemented
```

> Response for get all requests

```json
[{
   "id": 1,
   "entity_name": "Test 1",
   "legal_number": "77.777.777-7",
   "missing_records": "Falta antecedente numero 1",
   "lawyer": "Example Lawyer"
},
   {
     "id": 2,
     "entity_name": "Test 2",
     "legal_number": "88.888.888-8",
     "missing_records": null,
     "lawyer_id": null
   }]
```

### GET REQUEST
  <p><span class="label label-info">GET</span>/requests/<code>{request_id}</code></p>
  <p><strong>URL Parameters</strong></p>
  
  Parameter | Type | Example | Description
  --------- | ---- | ------- | -----------
  request_id|integer|1|ID of specific client' request
  
> Example for get request

```shell
  curl -X GET "https://app.oxalis.cl/api/v1/requests/1" \
    -H "username: company_username" \
    -H "password: company_password"
```

```ruby
    require 'rest-client'
    require 'json'
    
   response = RestClient::Request.execute(method: :get,
                                          url: 'http://app.oxalis.cl/api/v1/requests/1',
                                          headers: { username: 'company_username',
                                                     password: 'company_password'})
   result = JSON.parse(response) 
   result
```

```javascript
  // not implemented
```

> Response for get request

```json
{
  "id": 1,
  "entity_name": "Test 1",
  "legal_number": "77.777.777-7",
  "missing_records": "test en producción",
  "lawyer": "Example Lawyer"
}
```

### CREATE REQUEST
  <p><span class="label label-info">POST</span>/requests</p>
  <p><strong>URL Parameters</strong></p>
  
  Parameter | Type | Example | Description
  --------- | ---- | ------- | -----------
  request_id|integer|1|ID to create client' request
  
  <p><strong>Form Data</strong></p>
  
  Parameter | Type | Example
  --------- | ---- | -------
  rut|string|77.777.777-7
  name|string|Example Society
  documents|array[string]|["http://example.com/document1.pdf", "http://example.com/document2.pdf"]

  <aside class="notice">
   The files that are sent in the <code>documents</code> attribute must be in <strong>PDF</strong> format.
  </aside>
  
> Example for create request

```shell
  curl -X POST "https://app.oxalis.cl/api/v1/requests" \
    -H "username: company_username" \
    -H "password: company_password"
```

```ruby
  require 'rest-client'
  require 'json'
   
  response = RestClient::Request.execute(method: :post,
                                         url: 'http://app.oxalis.cl/api/v1/requests',
                                         headers: { username: 'company_username',
                                                    password: 'company_password'})
  result = JSON.parse(response) 
  result
```

```javascript
  // not implemented
```

> Response for create request

```json
{
  "request_id": 1,
  "message": "Request created successfully"
}
```

### GET REQUEST STATUS
  <p><span class="label label-info">GET</span>/requests/<code>{request_id}</code>/status</p>
  <p><strong>URL Parameters</strong></p>
  
  Parameter | Type | Example | Description
  --------- | ---- | ------- | -----------
  request_id|integer|1|ID of specific client' request
  
> Example for get request status

```shell
  curl -X GET "https://app.oxalis.cl/api/v1/requests/1/status" \
    -H "username: company_username" \
    -H "password: company_password"
```

```ruby
  require 'rest-client'
  require 'json'
   
  response = RestClient::Request.execute(method: :get,
                                         url: 'https://app.oxalis.cl/api/v1/requests/1/status',
                                         headers: { username: 'company_username',
                                                    password: 'company_password'})
  result = JSON.parse(response) 
  result
```

```javascript
  // not implemented
```

> Response for get request status

```json
{
  "request_id": 1,
  "status": "requested"
}
```

### COMPLEMENT REQUEST
  <p><span class="label label-info">POST</span>/requests/<code>{request_id}</code>/complement</p>
  <p><strong>URL Parameters</strong></p>
  
  Parameter | Type | Example | Description
  --------- | ---- | ------- | -----------
  request_id|integer|1|ID to create client' request
  
  <p><strong>Form Data</strong></p>
  
  Parameter | Type | Example
  --------- | ---- | -------
  documents|array[string]|["http://example.com/document1.pdf", "http://example.com/document2.pdf"]

  <aside class="notice">
   The files that are sent in the <code>documents</code> attribute must be in <strong>PDF</strong> format.
  </aside>
  
> Example for complement request

```shell
  curl -X POST "https://app.oxalis.cl/api/v1/requests/1/complement" \
    -H "username: company_username" \
    -H "password: company_password"
```

```ruby
  require 'rest-client'
  require 'json'
   
  response = RestClient::Request.execute(method: :post,
                                         url: 'https://app.oxalis.cl/api/v1/requests/1/complement',
                                         headers: { username: 'company_username',
                                                    password: 'company_password'})
  result = JSON.parse(response) 
  result
```

```javascript
  // not implemented
```

> Response for complement request

```json
{
  "request_id": 1,
  "message": "Request complemented successfully"
}
```

### GET REQUEST REPORT
  <p><span class="label label-info">GET</span>/requests/<code>{request_id}</code>/report</p>
  <p><strong>URL Parameters</strong></p>
  
  Parameter | Type | Example | Description
  --------- | ---- | ------- | -----------
  
> Example for get request report

```shell
  curl -X GET "https://app.oxalis.cl/api/v1/requests/1/report" \
    -H "username: company_username" \
    -H "password: company_password"
```

```ruby
  require 'rest-client'
  require 'json'
   
  response = RestClient::Request.execute(method: :get,
                                         url: 'https://app.oxalis.cl/api/v1/requests/1/report',
                                         headers: { username: 'company_username',
                                                    password: 'company_password'})

```

```javascript
  // not implemented
```

> Response for get request report

```text
  Download document
```
