# API Documentation

## Base URLs
- **HTTP project-service**: `https://domain:3001/api/v1`
- **HTTP file-service**: `https://domain:3002/api/v1`
- **HTTP discord-auth-service**: `https://domain:3003/api/v1`
---

## Authentication
- **Method**: Bearer Token
- **Details**: All API requests require a valid Discord user token for authentication.
  - **HTTP**: Include the token in the `Authorization` header as `Bearer <discord_token>`.

---

## HTTP project-service

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
            "limit": "integer"
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
    { "error": "Name is required" }
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
            "limit": "integer"
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
            "limit": "integer"
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
                "styleId": "integer"
            }
        ],
        "pagination": {
            "lastPage": "integer",
            "limit": "integer"
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
    "styleId": "integer",
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
      "styleId": "integer",
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
      "styleId": "integer",
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
  
#### PUT `/projects/{projectId}/boards/{boardId}/lists/{listId}/cards/{cardId}/order`
- Update the order of a specific card.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `listId`: ID of the list.
  - `cardId`: ID of the card.
- **Body**:
  ```json
  {
    "order": "integer"
  }
  ```
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Missing required parameters or order" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Card not found" }
    ```
  - **500 Internal Server Error**:
    ```json
    { "error": "Error updating order" }
    ```

#### PUT `/projects/{projectId}/boards/{boardId}/lists/{listId}/cards/{cardId}/reminder-interval`
- Update the reminder interval of a specific card.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `listId`: ID of the list.
  - `cardId`: ID of the card.
- **Body**:
  ```json
  {
    "reminderDaysInterval": "integer"
  }
  ```
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Missing required parameters or reminderDaysInterval" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Card not found" }
    ```
  - **500 Internal Server Error**:
    ```json
    { "error": "Error updating reminderDaysInterval" }
    ```

#### PUT `/projects/{projectId}/boards/{boardId}/lists/{listId}/cards/{cardId}/acknowledgements`
- Update acknowledgements for a specific card.
- **Path Parameters**:
  - `projectId`: ID of the project.
  - `boardId`: ID of the board.
  - `listId`: ID of the list.
  - `cardId`: ID of the card.
- **Body**:
  ```json
  {
    "acknowledgements": ["string"]
  }
  ```
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Missing required parameters or invalid acknowledgements format" }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Card not found" }
    ```
  - **500 Internal Server Error**:
    ```json
    { "error": "Error updating acknowledgements" }
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
            "limit": "integer"
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
      "styleId": "integer",
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
      "userIds": ["string"]
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

### **Invites**
#### POST `/projects/{projectId}/invite`
- Invite a user to a project.
- **Path Parameters**:
  - `projectId`: ID of the project to invite the user to.
- **Body**:
  ```json
  {
    "userId": "string",
  }
- **Response**:
  - **201 Created**:
    ```json
    {
      "success": true
    }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "Invalid input data" }
    ```
  - **401 Unauthorized**:
    ```json
    { "error": "Authentication required" }
    ```
  - **403 Forbidden**:
    ```json
    { "error": "You do not have permission to invite users to this project." }
    ```
  - **404 Not Found**:
    ```json
    { "error": "Project not found" }
    ```

---

### **Styles**
#### GET `/styles`
- Fetch a list of styles (categories) available for cards.

---

### **Response**

#### **200 OK**
```json
{
  "data": [
    {
      "styleId": "integer",
      "name": "string"
    },
    {
      "styleId": "integer",
      "name": "string"
    }
  ]
}
```
---

## HTTP file-service

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

#### DELETE `/file/{fileId}`
- Delete a file by its ID.
- **Path Parameters**:
  - `fileId`: ID of the file to delte.
- **Response**:
  - **200 OK**:
    ```json
    { "success": true }
    ```
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

## HTTP discord-auth-service

#### POST `/token`
- Invite a user to a project.
- **Body**:
  ```json
  {
    "code": "string",
  }
- **Response**:
  - **200 Ok**:
    ```json
    {
      "access_token": "string"
    }
    ```
  - **400 Bad Request**:
    ```json
    { "error": "string",  "error_description": "string"}
    ```
  - **500 Internal Server Error**:
    ```json
    { "error": "Unexpected server error" }
    ```
---

### Server-Sent Events (SSE)

#### SSE Endpoint
- **URL**: `/events?token={token}`
- **Method**: GET

---

### Event Types and Payloads

#### **Projects**
- **Event Type**: `project:created`
  - Sent when a new project is created.
  - **Payload**:
    ```json
    {
      "type": "project:created",
      "projectId": "integer",
      "name": "string"
    }
    ```

- **Event Type**: `project:updated`
  - Sent when a project is updated.
  - **Payload**:
    ```json
    {
      "type": "project:updated",
      "projectId": "integer",
      "name": "string"
    }
    ```

- **Event Type**: `project:deleted`
  - Sent when a project is deleted.
  - **Payload**:
    ```json
    {
      "type": "project:deleted",
      "projectId": "integer"
    }
    ```

---

#### **Boards**
- **Event Type**: `board:created`
  - Sent when a new board is created.
  - **Payload**:
    ```json
    {
      "type": "board:created",
      "projectId": "integer",
      "boardId": "integer",
      "name": "string"
    }
    ```

- **Event Type**: `board:updated`
  - Sent when a board is updated.
  - **Payload**:
    ```json
    {
      "type": "board:updated",
      "projectId": "integer",
      "boardId": "integer",
      "name": "string"
    }
    ```

- **Event Type**: `board:deleted`
  - Sent when a board is deleted.
  - **Payload**:
    ```json
    {
      "type": "board:deleted",
      "projectId": "integer",
      "boardId": "integer"
    }
    ```

---

#### **Lists**
- **Event Type**: `list:created`
  - Sent when a new list is created.
  - **Payload**:
    ```json
    {
      "type": "list:created",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "name": "string"
    }
    ```

- **Event Type**: `list:updated`
  - Sent when a list is updated.
  - **Payload**:
    ```json
    {
      "type": "list:updated",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "name": "string"
    }
    ```

- **Event Type**: `list:deleted`
  - Sent when a list is deleted.
  - **Payload**:
    ```json
    {
      "type": "list:deleted",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer"
    }
    ```

---

#### **Cards**
- **Event Type**: `card:created`
  - Sent when a new card is created.
  - **Payload**:
    ```json
    {
      "type": "card:created",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "cardId": "integer",
      "name": "string"
    }
    ```

- **Event Type**: `card:updated`
  - Sent when a card is updated.
  - **Payload**:
    ```json
    {
      "type": "card:updated",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "cardId": "integer",
      "name": "string"
    }
    ```

- **Event Type**: `card:deleted`
  - Sent when a card is deleted.
  - **Payload**:
    ```json
    {
      "type": "card:deleted",
      "projectId": "integer",
      "boardId": "integer",
      "listId": "integer",
      "cardId": "integer"
    }
    ```

