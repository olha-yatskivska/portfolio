### A matrix comparing the code's current behavior against industry standards

| Endpoint / Suite  | Scenario                                   | Expected Result according to the code|  Expected result according to the best practices standard                           | 
|-------------------|--------------------------------------------|--------------------------------------|------------------------------------------------------------------------------------ |
| System (Root)     | Ping the server (/ping)                    | 201 Created                          | 200 OK/204 No content  [REQ-BUG-01](./REQ-BUG-01)                                                             |
| System (Root)     | Request an invalid path (/foo/bar)         | 404 Not Found                        | 404 Not Found                                                                       |
| GET /booking      | Request all bookings                       | 200 OK, returns list of booking IDs  | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by firstname                        | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by lastname                         | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by checkin date                     | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by checkout date                    | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by checkin & checkout dates         | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter by name AND dates combined          | 200 OK, returns matching IDs         | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking      | Filter with invalid date format            | 500 Internal Server Error            | 400 Bad Request (client error responses) Bug report RE-002                          |
| GET /booking/{id} | Request specific booking ID (JSON Accept)  | 200 OK, returns JSON booking data    | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| GET /booking/{id} | Request specific booking ID (XML Accept)   | 200 OK, returns XML booking data     | 200 OK (if authorized) or 401/403 (if unauthorized/invalid token) Bug report RE-001 |
| POST /booking     | Submit valid JSON payload                  | 200 OK, assigns new ID               | 201 Created/200 OK, assigns new ID                                                  | 
| POST /booking     | Submit valid XML payload                   | 200 OK, assigns new ID               | 201 Created/200 OK, assigns new ID                                                  |  
| POST /booking     | Submit incomplete payload                  | 500 Internal Server Error            | 400 Bad Request (client error responses) Bug report RE-003                          |     
| POST /booking     | Submit multiple requests sequentially      | 200 OK, increments IDs correctly     | 200 OK, increments IDs correctly                                                    |
| POST /booking     | Submit valid payload, request XML response | 200 OK, returns XML payload          | 200 OK, returns XML payload                                                         |
| POST /booking     | Submit payload with extra/unmapped fields  | 200 OK, ignores extra fields         | 200 OK, ignores extra fields                                                        |
| POST /booking     | Request with invalid Accept header (/ogg)  | 418 I'm a Teapot                     | 400 Bad Request/406 Not Acceptable                                                  |    
| POST /auth        | Submit valid credentials                   | 200 OK, returns auth token           | 200 OK, returns auth token                                                          |
| POST /auth        | Submit invalid credentials                 | 200 OK, returns "Bad credentials"    | 401 Unauthorized                                                                    |
| PUT /booking      | Update booking without token               | 403 Forbidden                        | 401 Unauthorized                                                                    |
| PUT /booking      | Update booking with invalid token          | 403 Forbidden                        | 401 Unauthorized                                                                    |
| PUT /booking      | Update booking with valid token            | 200 OK, returns updated JSON         | 200 OK, returns updated JSON                                                        |    
| PUT /booking      | Update booking with Basic Auth header      | 200 OK, returns updated JSON         | 200 OK, returns updated JSON                                                        |
| PUT /booking      | Update non-existent booking ID             | 405 Method Not Allowed               | 404 Not Found (if authorized) or 401/403 (if unauthorized/invalid token)            |
| PUT /booking      | Update using XML payload                   | 200 OK, returns updated JSON         | 200 OK, returns updated JSON                                                        | 
| PUT /booking      | Update valid booking, request XML response | 200 OK, returns updated XML          | 200 OK, returns updated XML                                                         |
| DELETE /booking   | Delete booking without token               | 403 Forbidden                        | 401 Unauthorized                                                                    |
| DELETE /booking   | Delete booking with invalid token          | 403 Forbidden                        | 401 Unauthorized                                                                    |
| DELETE /booking   | Delete valid booking with token            | 201 Created                          | 204 No Content/200 OK                                                               |
| DELETE /booking   | Delete valid booking with Basic Auth       | 201 Created                          | 204 No Content/200 OK                                                               |
| DELETE /booking   | Delete non-existent booking ID             | 405 Method Not Allowed               | 404 Not Found (if authorized) or 401/403 (if unauthorized/invalid token)            |    
