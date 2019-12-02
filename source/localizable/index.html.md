---
title: API Documentación

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby

toc_footers:
  - <a href='https://app.oxalis.cl/users/sign_in'>Regístrese para obtener una clave de desarrollador</a>
  - <div>&#169; 2018 Corporate Legal Solutions</div>

includes:
  - errors

search: true
---

# Introducción

¡Bienvenido a la API de Oxalis2! Puede usar nuestra API para acceder a los endpoints de la API Oxalis2, que pueden obtener información de las solicitudes del cliente en nuestra base de datos.

Tenemos enlaces de lenguajes de programación Shell y Ruby! Puede ver ejemplos de código en el área de la derecha, y puede cambiar el lenguaje de programación de los ejemplos con las pestañas en la parte superior derecha.

# Versión
Versión: 1.0.0

URL: [Oxalis2 API](https://app.oxalis.cl/api/v1/)

# Solicitud de credenciales

Las credenciales deben ser solicitadas a Corporate Legal Solutions

# Autenticación

Oxalis2 utiliza el nombre de usuario y la contraseña de la API para permitir el acceso a la misma. Puedes conseguirlos en nuestro [Oxalis](http://oxalis.cl).

Oxalis espera que el nombre de usuario y la contraseña de la API se incluyan en todas las solicitudes al servidor en un encabezado similar al siguiente:

<aside class="notice">
 Debe reemplazar <code>username</code> y <code>password</code>  con su información personal para la API.
</aside>

# Autenticarse
<p class="explanation">
  Agregar los parámetros de autenticación en el <strong>Header</strong>
</p>

`Header: username` `Header: password`

<p><strong>URL Paráametros</strong></p>

Parámetro | Tipo | Ejemplo | Descripción
--------- | ---- | ------- | -----------
username|string|company_username|Usuario para usar los recursos de la API
password|string|company_password|Contraseña para usar los recursos de la API

> Asegúrese de reemplazar `username` y `password` con su nombre de usuario y contraseña para la API.

 <aside class="success">
   Recuerde — un usuario feliz es un usuario autenticado!
</aside>

# Gestión de solicitudes del cliente
  <p class="explanation">
  Esta sesión le permite gestionar las solicitudes del cliente.
  <span>Para comprender mejor, revise los ejemplos en diferentes lenguajes de programación.</span>
  </p> 

### OBTENER TODAS LAS SOLICITUDES
 <p><span class="label label-info">GET</span>/requests</p>
  <p><strong>URL Parámetros</strong></p>
  
 Parámetro | Tipo | Ejemplo | Descripción
  --------- | ---- | ------- | -----------
  
> Ejemplo para obtener todas las solicitudes

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

> Respuesta al obtener todas las solicitudes

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

### OBTENER SOLICITUD
  <p><span class="label label-info">GET</span>/requests/<code>{request_id}</code></p>
  <p><strong>URL Parámetros</strong></p>
  
  Parámetro | Tipo | Ejemplo | Descripción
  --------- | ---- | ------- | -----------
  request_id|integer|1|ID de la solicitud específica del cliente
  
> Ejemplo para obtener solicitud

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

> Respuesta al obtener solicitud

```json
{
  "id": 1,
  "entity_name": "Test 1",
  "legal_number": "77.777.777-7",
  "missing_records": "test en producción",
  "lawyer": "Example Lawyer"
}
```

### CREAR SOLICITUD
  <p><span class="label label-info">POST</span>/requests</p>
  <p><strong>URL Parámetros</strong></p>
  
  Parámetro | Tipo | Ejemplo | Descripción
  --------- | ---- | ------- | -----------
  request_id|integer|1|ID del cliente para crear la solicitud 
  
  <p><strong>Datos de formulario</strong></p>
  
  Parámetro | Tipo | Ejemplo
  --------- | ---- | -------
  rut|string|77.777.777-7
  name|string|Sociedad de ejemplo
  documents|array[string]|["http://example.com/document1.pdf", "http://example.com/document2.pdf"]

  <aside class="notice">
   Los archivos que se envían en el <code>documents</code> y deben estar en formato <strong>PDF</strong>.
  </aside>
  
> Ejemplo para crear solicitud

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

> Respuesta al crear solicitud

```json
{
  "request_id": 1,
  "message": "Request created successfully"
}
```

### OBTENER ESTADO DE SOLICITUD
  <p><span class="label label-info">GET</span>/requests/<code>{request_id}</code>/status</p>
  <p><strong>URL Parámetros</strong></p>
  
  Parámetro | Tipo | Ejemplo | Descripción
  --------- | ---- | ------- | -----------
  request_id|integer|1|ID de la solicitud específica del cliente
  
> Ejemplo para obtener el estado de la solicitud

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

> Respuesta al obtener el estado de la solicitud

```json
{
  "request_id": 1,
  "status": "requested"
}
```

### SOLICITUD DE COMPLEMENTO
  <p><span class="label label-info">POST</span>/requests/<code>{request_id}</code>/complement</p>
  <p><strong>URL Parámetros</strong></p>
  
  Parámetro | Tipo | Ejemplo | Descripción
  --------- | ---- | ------- | -----------
  request_id|integer|1|ID de la solicitud del cliente
  
  <p><strong>Form Data</strong></p>
  
  Parámetro | Tipo | Ejemplo
  --------- | ---- | -------
  documents|array[string]|["http://example.com/document1.pdf", "http://example.com/document2.pdf"]

  <aside class="notice">
   Los archivos que se envían en el <code>documents</code> y deben estar en formato <strong>PDF</strong>.
  </aside>
  
> Ejemplo de solicitud de complemento

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

> Response for complement request

```json
{
  "request_id": 1,
  "message": "Request complemented successfully"
}
```

### OBTENER INFORME DE SOLICITUD
  <p><span class="label label-info">GET</span>/requests/<code>{request_id}</code>/report</p>
  <p><strong>URL Parámetros</strong></p>
  
  Parámetro | Tipo | Ejemplo | Descripción
  --------- | ---- | ------- | -----------
  
> Ejemplo para obtener un informe de solicitud

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

> Respuesta al obtener el informe de solicitud

```text
  Descargar documento
```
