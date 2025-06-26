What is a REST API?
REST (Representational State Transfer) is an architectural style for designing web services. A RESTful API allows clients (like web or mobile apps) to interact with server-side resources over HTTP using standardized operations like GET , POST , PUT , PATCH , DELETE.

___________________________________


RESTful architecture principles:

1. Client-Server Architecture
   The client and server are separate entities , Client (frontend) and server (backend) are separate systems that interact through requests and responses.

2. Stateless
	Each request from the client to the server must contain all the information needed to understand and process the request No session state is stored on the server.
3. Uniform Interface
	Standardized method of communication between client and server using resources (e.g., using HTTP methods like GET, POST, PUT, DELETE).

4. Cacheable
	Responses must define themselves as cacheable or not to improve performance.
5. Layered System
	Clients don't need to know whether they are connected directly to the server or through an intermediary (e.g., a load balancer or proxy).

6. Code on Demand (Optional)
	Servers can send executable code to clients (like JavaScript) to extend their functionality.

__________________________________________


CRUD operations 

| CRUD Operation | HTTP Method   | Purpose             | Example Endpoint               |
| -------------- | ------------- | ------------------- | ------------------------------ |
| **Create**     | `POST`        | Create a resource   | `POST /users`                  |
| **Read**       | `GET`         | Retrieve a resource | `GET /users` or `GET /users/5` |
| **Update**     | `PUT`/`PATCH` | Update resource     | `PUT /users/5`                 |
| **Delete**     | `DELETE`      | Remove resource     | `DELETE /users/5`              |

____________________________________________


Role of URIs, request headers, request bodies


URI (Uniform Resource Identifier)

> The address used to identify the resource being acted upon.
> Locates the resource (like a file path or ID)
Examples:
URI			Meaning
/users			Refers to the collection of all users
/users/101		Refers to the user with ID 101
/products/45/reviews	Reviews of product with ID 45


Headers
>Key-value pairs sent with the request/response to pass meta-information.
>Define content type, auth, language, caching, etc.

Common Request Headers:
Header					Use Case
Content-Type: application/json		Declares that the request body is in JSON format
Authorization: Bearer <token>		Used for sending JWTs or access tokens
Accept: application/json		Client wants JSON in response
User-Agent: Mozilla/5.0			Info about the client making the request


Request Body (Payload)
>The request body contains the actual data being sent to the server (used mainly with POST, PUT, and PATCH requests).
>Creating or updating a resource
>Submitting form or file data

Supported content types:
application/json (most common)
multipart/form-data (for file uploads)


_______________________________________________

Meaning and use of common HTTP status codes:

200 	OK		The request was successful, and the response contains the requested data.

Use Case:
GET /users/123 → Returns user data
PUT /users/123 → Updates user and returns updated data


201 	Created		The request was successful, and a new resource has been created.

Use Case:
POST /users → Creates a new user
Response typically includes a Location header pointing to the new resource (/users/124)


204 	No Content	The request was successful, but there is no content to return.

Use Case:
DELETE /users/123 → Successfully deletes the user, no body needed
PUT or PATCH request that succeeds but doesn’t return updated data


Client Error Codes
400 	Bad Request	The server could not understand the request due to invalid syntax or missing/incorrect data.

Use Case:
Sending a malformed JSON body or missing required fields
POST /users with invalid email format


401 	Unauthorized	 The request requires authentication, but the client is not authenticated.

Use Case:
Missing or invalid JWT/token in the Authorization header
Attempting to access protected resources without logging in


403	 Forbidden	The client is authenticated, but does not have permission to access the resource.

Use Case:
Authenticated user trying to access an admin-only API
Example: Regular user tries DELETE /users/1


404 	Not Found	The requested resource does not exist on the server.

Use Case:
GET /users/9999 → User ID doesn’t exist
Mistyped or incorrect URL


409 	Conflict	The request could not be completed due to a conflict with the current state of the resource.

Use Case:
Attempting to create a user with an email that already exists
Resource version conflict in concurrent updates


Server Error Code
500 	Internal Server Error	The server encountered an unexpected error while processing the request.

Use Case:
Code exceptions, unhandled errors, misconfigurations
Should be logged and investigated




Status Code			Meaning						Typical Use Case
200 OK				Request succeeded				Successful GET, PUT, or POST
201 Created			New resource created				Successful POST (e.g., create user)
204 No Content			Success, no response body			Successful DELETE, PUT without return data
400 Bad Request			Client sent invalid request			Missing fields, malformed JSON
401 Unauthorized		Authentication required/failed			Missing or invalid token
403 Forbidden			Not allowed, despite being logged in		Authenticated but no permission
404 Not Found			Resource doesn't exist				Wrong ID or endpoint
409 Conflict			Conflict with existing state			Duplicate entries, concurrency issues
500 Server Error		Server crashed or failed unexpectedly		Bug, exception, or crash on server






