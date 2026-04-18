# Quickstart Guide: Physical AI & Humanoid Robotics Course Textbook with RAG Chatbot

**Feature Branch**: `001-course-textbook-rag`  
**Created**: 2026-04-18  
**Purpose**: Provide instructions for quickly setting up and running the textbook and RAG chatbot locally.

## 1. Prerequisites

*   **Python 3.9+**
*   **Node.js (LTS)** and **npm/yarn** (for Docusaurus)
*   **Docker** (Optional, for local database/vector database setup)
*   **OpenAI API Key**: Required for the RAG chatbot's OpenAI Agents SDK.
*   **Neon Serverless Postgres Account**: Free tier is sufficient.
*   **Qdrant Cloud Account**: Free tier is sufficient.

## 2. Setup

### 2.1. Clone the Repository

```bash
git clone <repository-url>
cd <repository-name>
```

### 2.2. Backend (FastAPI & RAG Chatbot)

1.  **Navigate to backend directory**:
    ```bash
    cd backend
    ```
2.  **Create a Python Virtual Environment**:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: .\venv\Scripts\activate
    ```
3.  **Install Python Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```
    (Note: `requirements.txt` will be created during implementation, containing `fastapi`, `uvicorn`, `openai-sdk`, `qdrant-client`, `psycopg2-binary`, etc.)

4.  **Configure Environment Variables**:
    Create a `.env` file in the `backend/` directory with the following:
    ```
    OPENAI_API_KEY="your_openai_api_key"
# To use other LLMs (e.g., Gemini) with OpenAI Agents SDK, you might need to change the API key
# and potentially the API base URL depending on the SDK's configuration for the chosen provider.
# Example for Gemini (requires specific SDK setup):
# GEMINI_API_KEY="your_gemini_api_key"
# OPENAI_API_BASE="https://api.example.com/v1" # Adjust if your LLM provider has a compatible API endpoint
    DATABASE_URL="your_neon_postgres_connection_string"
    QDRANT_URL="your_qdrant_cloud_url"
    QDRANT_API_KEY="your_qdrant_api_key"
    ```

5.  **Run Database Migrations (if applicable)**:
    ```bash
    # Command to run database migrations (e.g., using Alembic or custom script)
    ```

6.  **Ingest Textbook Content into Qdrant**: (This step will involve a script to parse Docusaurus content and vectorize it)
    ```bash
    python scripts/ingest_content.py  # Example command
    ```

7.  **Start the FastAPI Backend Server**:
    ```bash
    uvicorn main:app --reload --port 8000
    ```
    The API will be available at `http://localhost:8000`.

### 2.3. Frontend (Docusaurus Textbook)

1.  **Navigate to frontend directory**:
    ```bash
    cd frontend
    ```
2.  **Install Node.js Dependencies**:
    ```bash
    npm install # or yarn install
    ```
3.  **Configure API Endpoint**: 
    Edit `docusaurus.config.js` or an equivalent configuration file to point to your FastAPI backend (e.g., `http://localhost:8000`).

4.  **Start the Docusaurus Development Server**:
    ```bash
    npm start # or yarn start
    ```
    The textbook will be available at `http://localhost:3000`.

## 3. Usage

1.  Open your web browser to `http://localhost:3000` to access the textbook.
2.  Navigate through modules using the sidebar or search functionality.
3.  Interact with the embedded RAG chatbot (usually a UI component on each page) by typing questions.
4.  To use the selected text query feature, highlight text in the textbook and then initiate a chatbot query; the UI should provide an option to query on selected text.

## 4. Deployment (Overview)

*   **Frontend (Docusaurus)**: Deploy to GitHub Pages or a similar static site hosting service.
*   **Backend (FastAPI)**: Deploy to a cloud platform like Render, Vercel, AWS EC2, Google Cloud Run, or Azure App Service.
*   Ensure environment variables (`OPENAI_API_KEY`, `DATABASE_URL`, `QDRANT_URL`, `QDRANT_API_KEY`) are correctly configured in the deployment environment.
