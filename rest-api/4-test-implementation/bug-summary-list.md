| Identifier | Title                                                                                                        |
| ---------- | ------------------------------------------------------------------------------------------------------------ |
| SCH-BUG-01 | [GET /ping] endpoint returns HTTP status 201 Created instead of 200 OK Linked to: REQ-BUG-01                 |
| SCH-BUG-02 | GetBookingIds by checkin/checkout date returns an empty array [] - BVA checkin does not include min boundary |
| SCH-BUG-03 | GetBooking returns in response wrong Content-Type in Header when requesting application/xml                  |
| SCH-BUG-04 | API returns 200 OK with unhandled JS exception body when requesting application/x-www-form-urlencoded        |
| SCH-BUG-05 | CreateToken 200 with message "reason": "Bad credentials" for misssing/empty data                             |
| SCH-BUG-06 | [DELETE/booking] returns 201 Created instead of 200 OK or 204 No Content Linked to: REQ-BUG-02               |
| SCH-BUG-07 | CreateBooking : XML deserialization layer on the server: "depositpaid": false returns true<br>               |
| SCH-BUG-08 | [GET /booking] Invalid checkin/checkout date format causes 500 error                                         |
| SCH-BUG-09 | [POST/PUT /booking] Invalid data type in additionalneeds field is accepted with 200 OK                       |
| SCH-BUG-10 | [PATCH /booking] Partial update of checkin date corrupts checkout to "0NaN-aN-aN" breaking contract schema   |
| SCH-BUG-11 | [POST /booking] Missing input validation causes 500 error on omitted mandatory fields                        |
| SCH-BUG-12 | [DELETE /booking/:id] Returns 405 Method Not Allowed when deleting non-existent entity or invalid format     |
| SCH-BUG-13 | [POST /PUT/booking] Missing validation for name fields leads to 500 Internal Server Error                    |
| SCH-BUG-14 | [POST /PUT/booking] UpdateBooking with wrong format for totalprice returnes 200 with null                    |
| SCH-BUG-15 | [POST /PUT/booking] Depositpaid field always evaluates to true for any non-zero value                        |
| SCH-BUG-16 | [POST/PUT/booking] Invalid checkin/checkout data type causes date corruption to display as '0NaN-aN-aN'      |
