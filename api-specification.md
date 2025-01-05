# API Documentation

## Base URLs
- **HTTP project-service**: `https://domain:5000/api/v1`
- **HTTP file-service**: `https://domain:3000/api/v1`
---

## Authentication
- **Method**: Bearer Token
- **Details**: All API requests require a valid Discord user token for authentication.
  - **HTTP**: Include the token in the `Authorization` header as `Bearer <discord_token>`.

---

## HTTP APIs

### **Projects**
#### GET `/projects/{projectId}`
- Fetch details of a specific project.
- **Path Parameters**:
  - projectId: ID of the project.
- **Response**:
  - **200 OK**:
    ```json
    {
      "projectId": "integer",
      "name": "string",
      "description": "string"
    }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Project not found" }
    ```

#### GET `/projects?page={page}&limit={limit}`
- Fetch a paginated list of projects accessible to the user.
- **Query Parameters**:
  - `page` (optional): Page number.
  - `limit` (optional): Number of items per page.
- **Response**:
  - **200 OK**:
    ```json
    {   
        "data": [
            {
                "projectId": "integer",
                "name": "string",
                "description": "string"
            },
            {
                "projectId": "integer",
                "name": "string",
                "description": "string"
            }
        ],
        "pagination": {
            "lastPage": "integer",
        }
    }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```

#### POST `/projects`
- Create a new project.
- **Body**:
  ```json
  {
    "name": "string",
    "description": "string"
  }
  ```
- **Response**:
  - **201 Created**:
    ```json
    { "projectId": "integer" }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Invalid input data" }
    ```

#### PUT `/projects/{projectId}`
- Update details of a specific project.
- **Path Parameters**:
  - `projectId`: ID of the project to update.
- **Body**:
  ```json
  {
    "name": "string",
    "description": "string"
  }
  ```
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Project not found" }
    ```

#### DELETE `/projects/{projectId}`
- Delete a specific project.
- **Path Parameters**:
  - `projectId`: ID of the project to delete.
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Project not found" }
    ```

---

### **Boards**
#### GET `/projects/{projectId}/boards/{boardId}`
- Fetch details of a specific board within a project.
- **Path Parameters**:
  - projectId: ID of the project.
  - boardId: ID of the board.
- **Response**:
  - **200 OK**:
    ```json
    {
      "boardId": "integer",
      "name": "string",
      "description": "string"
    }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Board not found" }
    ```

#### GET `/projects/{projectId}/boards?page={page}&limit={limit}`
- Fetch a paginated list of boards within a project.
- **Path Parameters**:
  - `projectId`: ID of the project.
- **Query Parameters**:
  - `page` (optional): Page number.
  - `limit` (optional): Number of items per page.
- **Response**:
  - **200 OK**:
    ```json
    {   
        "data": [
            {
                "boardId": "integer",
                "name": "string",
                "description": "string"
            },
            {
                "boardId": "integer",
                "name": "string",
                "description": "string"
            }
        ],
        "pagination": {
            "lastPage": "integer",
        }
    }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Project not found" }
    ```

#### POST `/projects/{projectId}/boards`
- Create a new board within a project.
- **Path Parameters**:
  - `projectId`: ID of the project.
- **Body**:
  ```json
  {
    "name": "string",
    "description": "string"
  }
  ```
- **Response**:
  - **201 Created**:
    ```json
    { "boardId": "integer" }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Invalid input data" }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```

#### PUT `/projects/{projectId}/boards/{boardId}`
- Update details of a specific board.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board to update.
- **Body**:
  ```json
  {
    "name": "string",
    "description": "integer"
  }
  ```
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Board not found" }
    ```

#### DELETE `/projects/{projectId}/boards/{boardId}`
- Delete a specific board.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board to delete.
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Board not found" }
    ```

---

### **Lists**
#### GET `/projects/{projectId}/boards/{boardId}/lists/{listId}`
- Fetch details of a specific list within a board.
- **Path Parameters**:
  - projectId: ID of the project.
  - boardId: ID of the board.
  - listId: ID of the list.
- **Response**:
  - **200 OK**:
    ```json
    {
      "listId": "integer",
      "name": "string"
    }
    ```
  - **404 Not Found**:
    ```json
    { "error": "List not found" }
    ```

#### GET `/projects/{projectId}/boards/{boardId}/lists?page={page}&limit={limit}`
- Fetch a paginated list of lists within a board.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
- **Query Parameters**:
  - `page` (optional): Page number.
  - `limit` (optional): Number of items per page.
- **Response**:
  - **200 OK**:
    ```json
    {   
        "data": [
            {
                "listId": "integer",
                "name": "string"
            },
            {
                "listId": "integer",
                "name": "string"
            }
        ],
        "pagination": {
            "lastPage": "integer",
        }
    }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Board  not found" }
    ```

#### POST `/projects/{projectId}/boards/{boardId}/lists`
- Create a new list within a board.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
- **Body**:
  ```json
  {
    "name": "string",
    "order": "integer"
  }
  ```
- **Response**:
  - **201 Created**:
    ```json
    { "listId": "integer" }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Invalid input data" }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```

#### PUT `/projects/{projectId}/boards/{boardId}/lists/{listId}`
- Update details of a specific list.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `listId`: ID of the list.
- **Body**:
  ```json
  {
    "name": "string"
  }
  ```
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "List not found" }
    ```

#### DELETE `/projects/{projectId}/boards/{boardId}/lists/{listId}`
- Delete a specific list.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `listId`: ID of the list.
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "List not found" }
    ```

---

### **Cards**
#### GET `/projects/{projectId}/boards/{boardId}/lists/{listId}/cards?page={page}&limit={limit}`
- Fetch a paginated list of cards within specific lists of a board.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `listId` : ID for the lists to fetch cards from.
- **Query Parameters**:
  - `page` (optional): Page number.
  - `limit` (optional): Number of items per page.
- **Response**:
  - **200 OK**:
    ```json
    {
        "data": [
            {
                "cardId": "integer",
                "listId": "integer",
                "name": "string",
                "startDate": "string",
                "endDate": "string",
                "assignedTo": ["string"],
                "style": "string"
            }
        ],
        "pagination": {
            "lastPage": "integer",
        }
    }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Invalid list id" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "List not found" }
    ```

#### POST `/projects/{projectId}/boards/{boardId}/cards`
- Create a new card within a board.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
- **Body**:
  ```json
  {
    "listId": "integer",
    "name": "string",
    "description": "string",
    "style": "string",
    "startDate": "string",
    "endDate": "string",
    "reminderDaysInterval": "integer",
    "assignedTo": ["string"],
    "files": [
        {
            "name": "string",
            "fileId": "integer"
        }
    ]
  }
  ```
- **Response**:
  - **201 Created**:
    ```json
    { "cardId": "integer" }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Invalid input data" }
    ```

#### GET `/projects/{projectId}/boards/{boardId}/cards/{cardId}`
- Fetch details of a specific card.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `cardId`: ID of the card.
- **Response**:
  - **200 OK**:
    ```json
    {
      "cardId": "integer",
      "name": "string",
      "description": "string",
      "style": "string",
      "startDate": "string",
      "endDate": "string",
      "reminderDaysInterval": "integer",
      "assignedTo": ["string"],
      "files": [
          {
              "name": "string",
              "fileId": "integer"
          }
      ],
      "acknowledgements": [
        {
            "userId": "string",
            "isAcknowledged": "boolean"
        }
      ]
    }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Card not found" }
    ```

#### PUT `/projects/{projectId}/boards/{boardId}/cards/{cardId}`
- Update details of a specific card.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `cardId`: ID of the card.
- **Body**:
  ```json
    {
      "name": "string",
      "description": "string",
      "style": "string",
      "startDate": "string",
      "endDate": "string",
      "reminderDaysInterval": "integer",
      "assignedTo": ["string"],
      "files": [
          {
              "name": "string",
              "fileId": "integer"
          }
      ],
      "acknowledgements": [
        {
            "userId": "string",
            "isAcknowledged": "boolean"
        }
      ]
    }
  ```
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Card not found" }
    ```

#### DELETE `/projects/{projectId}/boards/{boardId}/cards/{cardId}`
- Delete a specific card.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `cardId`: ID of the card.
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Card not found" }
    ```

---

### **Card Histories**
#### GET `/projects/{projectId}/boards/{boardId}/lists/{listId}/cards/{cardId}/histories?page={page}&limit={limit}`
- Fetch a paginated list of histories for a specific card.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `cardId`: ID of the card.
- **Query Parameters**:
  - `page` (optional): Page number.
  - `limit` (optional): Number of items per page.
- **Response**:
  - **200 OK**:
    ```json
    {
        "data": [
            {
                "versionNumber": "integer",
                "name": "string",
                "description": "string",
                "addedNFile": "integer",
                "deletedNFile": "integer",
                "startDate": "string",
                "endDate": "string",
                "assignedTo": ["string"],
                "styleIsChanged": "boolean",
                "versionDate": "string",
            }
        ],
        "pagination": {
            "lastPage": "integer",
        }
    }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Invalid card Id" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Card not found" }
    ```

#### GET `/projects/{projectId}/boards/{boardId}/lists/{listId}/cards/{cardId}/histories/{versionNumber}`
- Fetch details of a specific history entry for a card.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `cardId`: ID of the card.
  - `versionNumber`: ID of the history entry.
- **Response**:
  - **200 OK**:
    ```json
    {
      "versionNumber": "integer",
      "name": "string",
      "description": "string",
      "style": "string",
      "startDate": "string",
      "endDate": "string",
      "assignedTo": ["string"],
      "files": [
          {
              "name": "string",
              "fileId": "integer"
          }
      ]
    }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Invalid card history Id" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Card history not found" }
    ```

---

### **Members**

#### GET /projects/{projectId}/members
- Fetch a list of user IDs (members) for a specific project.
- **Path Parameters**:
  - projectId: ID of the project.
- **Response**:
  - **200 OK**:
    ```json
    {
      "data": [
        {
          "userId": "string",
        },
        {
          "userId": "string",
        }
      ]
    }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Project not found" }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```
---

### **Files**

#### GET `/file/{fileId}`
- Retrieve a file by its ID.
- **Path Parameters**:
  - `fileId`: ID of the file to retrieve.
- **Response**:
  - **200 OK**:
    - **Content-Type**: application/octet-stream (or appropriate MIME type)
    - **Body**: The file content.
  - **400 Bad Request**:
    ```json
    { "error": "Invalid fileId format" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "File not found" }
    ```
  - **500 Internal Server Error**:
    ```json
    { "error": "Unexpected server error" }
    ```

#### POST `/file/upload`
- Upload a new file.
- **Request Body**:
  - **Content-Type**: multipart/form-data
  - **Body**: The file to be uploaded (via form-data).
- **Response**:
  - **201 Created**:
    ```json
    {
      "fileId": "integer"
    }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Invalid file format or missing file" }
    ```
  - **413 Payload Too Large**:
    ```json
    { "error": "File size exceeds limit" }
    ```
  - **500 Internal Server Error**:
    ```json
    { "error": "Unexpected error during file upload" }
    ```

---

## SSE APIs

### **Initial Connection**
#### Authentication
When establishing a Server-Sent Events (SSE) connection, the client must authenticate by providing a valid Discord OAuth2 access token. The token must be included as a query parameter in the connection URL:

- **Connection URL**:
  ```plaintext
  /events?token=<ACCESS_TOKEN>
  ```

#### Server Response
The server validates the token by calling Discord's `/users/@me` API. Based on the result:

- **Successful Authentication**:
  The server keeps the connection open and begins streaming events.

- **Failed Authentication**:
  The server responds with an HTTP 401 status and closes the connection.

---

### **Projects**
#### Events
- **`created`**
  - Sent when a new project is created.
  - **Path**: `/events/projects`
  - **Payload**:
    ```json
    {
      "type": "created",
      "projectId": "integer",
      "name": "string",
      "createdAt": "string"
    }
    ```

- **`updated`**
  - Sent when a project is updated.
  - **Path**: `/events/projects`
  - **Payload**:
    ```json
    {
      "type": "updated",
      "projectId": "integer",
      "name": "string",
      "updatedAt": "string"
    }
    ```

- **`deleted`**
  - Sent when a project is deleted.
  - **Path**: `/events/projects`
  - **Payload**:
    ```json
    {
      "type": "deleted",
      "projectId": "integer"
    }
    ```

---

### **Boards**
#### Events
- **`created`**
  - Sent when a new board is created in a project.
  - **Path**: `/events/boards`
  - **Payload**:
    ```json
    {
      "type": "created",
      "projectId": "integer",
      "boardId": "integer",
      "name": "string",
      "createdAt": "string"
    }
    ```

- **`updated`**
  - Sent when a board in a project is updated.
  - **Path**: `/events/boards`
  - **Payload**:
    ```json
    {
      "type": "updated",
      "projectId": "integer",
      "boardId": "integer",
      "name": "string",
      "updatedAt": "string"
    }
    ```

- **`deleted`**
  - Sent when a board in a project is deleted.
  - **Path**: `/events/boards`
  - **Payload**:
    ```json
    {
      "type": "deleted",
      "projectId": "integer",
      "boardId": "integer"
    }
    ```

---

### **Lists**
#### Events
- **`created`**
  - Sent when a new list is created in a board.
  - **Path**: `/events/lists`
  - **Payload**:
    ```json
    {
      "type": "created",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "name": "string",
      "createdAt": "string"
    }
    ```

- **`updated`**
  - Sent when a list in a board is updated.
  - **Path**: `/events/lists`
  - **Payload**:
    ```json
    {
      "type": "updated",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "name": "string",
      "updatedAt": "string"
    }
    ```

- **`deleted`**
  - Sent when a list in a board is deleted.
  - **Path**: `/events/lists`
  - **Payload**:
    ```json
    {
      "type": "deleted",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer"
    }
    ```

---

### **Cards**
#### Events
- **`created`**
  - Sent when a new card is created in a list.
  - **Path**: `/events/cards`
  - **Payload**:
    ```json
    {
      "type": "created",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "cardId": "integer",
      "name": "string",
      "createdAt": "string"
    }
    ```

- **`updated`**
  - Sent when a card is updated in a list.
  - **Path**: `/events/cards`
  - **Payload**:
    ```json
    {
      "type": "updated",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "cardId": "integer",
      "name": "string",
      "updatedAt": "string"
    }
    ```

- **`deleted`**
  - Sent when a card is deleted from a list.
  - **Path**: `/events/cards`
  - **Payload**:
    ```json
    {
      "type": "deleted",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "cardId": "integer"
    }
    ```

