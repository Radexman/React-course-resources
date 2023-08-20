# **API's & HTTP Requests**

What we have created in the previous section is a complete client side application all our feedback is hardcoded in the app and stored in the browser. In more realistic scenario we would have our data stored in some kind od database. We will use in this section API called JSONPlaceholder to make requests and get the data from the server.

## **Fullstack Application Overview**

-   Data is kept in a database on a server.
-   There is some kind of backend API (Written in any language).
-   The API has routes that we can access from the client (React) in order to create, read, update and delete data.
-   Data is brought into our state and used in our React app.

## **HTTP Methods**

-   GET - Retrieved data from the server.
-   POST - Submit data to the server.
-   PUT/PATCH - Update data already on the server.
-   DELETE - Delete data from the server.

## **HTTP Status Codes**

-   1xx - Informational - Request recieved/processing.
-   2xx - Success - Successfully recieved.
-   3xx - Redirect - Further action must be taken/redirect.
-   4xx - Client Error - Request does not have what it needs.
-   5xx - Server Error - Server failed to fulfill a valid request.
