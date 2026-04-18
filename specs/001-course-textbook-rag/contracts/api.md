# API Contracts: Physical AI & Humanoid Robotics Course Textbook with RAG Chatbot

**Feature Branch**: `001-course-textbook-rag`  
**Created**: 2026-04-18  
**Purpose**: Define the API endpoints for interaction between the Docusaurus frontend and the FastAPI backend.

## Endpoints

### 1. Get All Course Modules

*   **Endpoint**: `GET /modules`
*   **Description**: Retrieves a list of all course modules, including their IDs, titles, and order.
*   **Request**:
    *   `Headers`: None
    *   `Body`: None
*   **Response (200 OK)**:
    ```json
    [
        {
            "id": "uuid-module-1",
            "title": "Module 1: The Robotic Nervous System (ROS 2)",
            "order": 1,
            "slug": "module-1-ros2"
        },
        {
            "id": "uuid-module-2",
            "title": "Module 2: The Digital Twin (Gazebo & Unity)",
            "order": 2,
            "slug": "module-2-digital-twin"
        }
    ]
    ```
*   **Error Responses**:
    *   `500 Internal Server Error`: Generic error for server-side issues.

### 2. Get Course Module Content

*   **Endpoint**: `GET /modules/{module_id}`
*   **Description**: Retrieves the full content (markdown) of a specific course module.
*   **Request**:
    *   `Path Parameters`:
        *   `module_id` (UUID): The unique identifier of the module.
    *   `Headers`: None
    *   `Body`: None
*   **Response (200 OK)**:
    ```json
    {
        "id": "uuid-module-1",
        "title": "Module 1: The Robotic Nervous System (ROS 2)",
        "order": 1,
        "content": "# Module 1: The Robotic Nervous System (ROS 2)\n\n... (markdown content here) ...",
        "slug": "module-1-ros2"
    }
    ```
*   **Error Responses**:
    *   `404 Not Found`: If the `module_id` does not exist.
    *   `500 Internal Server Error`: Generic error for server-side issues.

### 3. Search Textbook Content

*   **Endpoint**: `GET /textbook/search`
*   **Description**: Performs a full-text search across the entire textbook content and returns relevant passages with highlights.
*   **Request**:
    *   `Query Parameters`:
        *   `q` (String, Required): The search query string.
    *   `Headers`: None
    *   `Body`: None
*   **Response (200 OK)**:
    ```json
    [
        {
            "module_id": "uuid-module-1",
            "module_title": "Module 1: The Robotic Nervous System (ROS 2)",
            "snippet": "...relevant passage with **highlighted** keyword...",
            "page_number": 5 (Optional)
        },
        {
            "module_id": "uuid-module-2",
            "module_title": "Module 2: The Digital Twin (Gazebo & Unity)",
            "snippet": "...another relevant passage...",
            "page_number": 12 (Optional)
        }
    ]
    ```
*   **Error Responses**:
    *   `400 Bad Request`: If `q` parameter is missing or empty.
    *   `500 Internal Server Error`: Generic error for server-side issues.

### 4. Query RAG Chatbot

*   **Endpoint**: `POST /chatbot/query`
*   **Description**: Sends a natural language query to the RAG chatbot and receives a context-aware answer. Supports optional selected text for focused queries.
*   **Request**:
    *   `Headers`: `Content-Type: application/json`
    *   `Body`:
        ```json
        {
            "query_text": "What are ROS 2 Nodes?",
            "selected_text_context": "[Optional] A selected paragraph or page content from the textbook for focused querying."
        }
        ```
*   **Response (200 OK)**:
    ```json
    {
        "response_text": "ROS 2 Nodes are ... (answer based on textbook or selected text).",
        "source_references": [
            "Module 1: The Robotic Nervous System (ROS 2)",
            "Page 3"
        ]
    }
    ```
*   **Error Responses**:
    *   `400 Bad Request`: If `query_text` is missing or invalid.
    *   `500 Internal Server Error`: Generic error for server-side issues.

