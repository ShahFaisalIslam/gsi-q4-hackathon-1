---

description: "Task list template for feature implementation"
---

# Tasks: Physical AI & Humanoid Robotics Course Textbook with RAG Chatbot

**Input**: Design documents from `/specs/001-course-textbook-rag/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/, quickstart.md

**Tests**: Tests are OPTIONAL and will only be generated if explicitly requested or if the spec implies testing is critical. In this case, user stories have independent test criteria defined, so test tasks will be generated where appropriate.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[TaskID] [P?] [Story?] Description with file path`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- **Web app**: `backend/src/`, `frontend/src/`, `backend/tests/`, `frontend/tests/`

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [ ] T001 Create project structure per implementation plan (backend/, frontend/, specs/)
- [ ] T002 Initialize Python project with FastAPI dependencies in `backend/requirements.txt`
- [ ] T003 Initialize Node.js project with Docusaurus dependencies in `frontend/package.json`
- [ ] T004 Configure linting and formatting tools (e.g., Black, Flake8 for Python; ESLint, Prettier for Node.js)
- [ ] T005 Set up basic connectivity checks for database (Neon) and vector database (Qdrant), and verify environment variables for AI agent API keys (OpenAI/Gemini) in `backend/src/config.py`
- [ ] T006 [P] Set up environment variables management (e.g., `.env` file for `OPENAI_API_KEY`, `DATABASE_URL`, `QDRANT_URL`, `QDRANT_API_KEY`)
- [ ] T007 [P] Set up database connection to Neon Serverless Postgres in `backend/src/db.py`
- [ ] T008 [P] Set up Qdrant client connection in `backend/src/vector_db.py`
- [ ] T009 Implement basic Docusaurus configuration (`docusaurus.config.js`) pointing to backend API placeholder

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [ ] T010 Implement basic error handling and logging middleware in `backend/src/middleware/error_handler.py`
- [ ] T011 Set up CORS configuration in `backend/src/main.py` for frontend access
- [ ] T012 Implement textbook content loading mechanism to read markdown files from Docusaurus structure into a usable format in `backend/src/services/textbook_loader.py`
- [ ] T013 Create initial data models (Course Textbook, Course Module) in `backend/src/models.py`
- [ ] T014 Write script to ingest textbook content into Qdrant vector database (`backend/scripts/ingest_content.py`)

**Checkpoint**: Foundation ready - user story implementation can now begin.

---

## Phase 3: User Story 1 - Access Course Content (Priority: P1) 🎯 MVP

**Goal**: Allow students to access and navigate the course textbook content.

**Independent Test**: Textbook content can be fully viewed and navigated.

### Implementation for User Story 1

- [ ] T015 [P] [US1] Create Docusaurus pages/routes for each module based on `course-details.md` in `frontend/docs/`
- [ ] T016 [P] [US1] Implement textbook navigation components (sidebar, next/prev buttons) in `frontend/src/components/`
- [ ] T017 [US1] Implement backend API endpoint to list all modules (`GET /modules`) in `backend/src/api/modules.py`
- [ ] T018 [US1] Implement backend API endpoint to get module content (`GET /modules/{module_id}`) in `backend/src/api/modules.py`
- [ ] T019 [US1] Integrate frontend navigation with backend API calls to fetch and display module content.

**Checkpoint**: User Story 1 is fully functional and independently testable.

---

## Phase 4: User Story 2 - Interact with RAG Chatbot for Course Queries (Priority: P1)

**Goal**: Enable students to ask questions to an embedded RAG chatbot that answers based on the textbook.

**Independent Test**: Chatbot accurately answers questions based *only* on the provided course material.

### Implementation for User Story 2

- [ ] T020 [P] [US2] Set up RAG pipeline: Integrate Qdrant for retrieval and OpenAI Agents SDK for generation in `backend/src/services/rag_chatbot.py`
- [ ] T021 [P] [US2] Develop chatbot backend endpoint (`POST /chatbot/query`) in `backend/src/api/chatbot.py`
- [ ] T022 [US2] Integrate chatbot UI component into Docusaurus frontend (`frontend/src/components/Chatbot.js`)
- [ ] T023 [US2] Implement logic to send student queries to the backend API and display responses.

**Checkpoint**: User Story 2 is fully functional and independently testable.

---

## Phase 5: User Story 5 - Query Chatbot on Selected Text (Priority: P1)

**Goal**: Allow students to select text and query the chatbot based on that selection.

**Independent Test**: Chatbot answers using only the selected text.

### Implementation for User Story 5

- [ ] T024 [P] [US5] Enhance chatbot backend to accept and process `selected_text_context` in the query endpoint (`POST /chatbot/query`).
- [ ] T025 [P] [US5] Implement frontend logic to capture selected text and pass it to the chatbot API.
- [ ] T026 [US5] Update chatbot response logic to prioritize selected text if provided.

**Checkpoint**: User Story 5 functionality is integrated.

---

## Phase 6: User Story 3 - Explore Course Modules (Priority: P2)

**Goal**: Provide a structured overview of course modules for navigation.

**Independent Test**: Module list is clear, and clicking modules navigates correctly.

### Implementation for User Story 3

- [ ] T027 [P] [US3] Implement backend API endpoint to list all modules (`GET /modules`) - *This might be covered by T016, ensure no duplication or create a specific task if distinct functionality is needed.*
- [ ] T028 [P] [US3] Update frontend to display the list of modules (e.g., in a sidebar or table of contents) and link them to module content.

**Checkpoint**: User Story 3 functionality is integrated.

---

## Phase 7: User Story 4 - Understand Hardware Requirements (Priority: P3)

**Goal**: Provide a dedicated section for hardware requirements.

**Independent Test**: Hardware requirements section is present and accurate.

### Implementation for User Story 4

- [ ] T029 [US4] Create a dedicated hardware requirements section in Docusaurus (`frontend/docs/hardware.md`).
- [ ] T030 [US4] Populate hardware requirements details from `course-details.md` into the new section.

**Checkpoint**: User Story 4 is implemented.

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Improvements affecting multiple user stories

- [ ] T031 [P] Update Docusaurus configuration for optimal performance and SEO (`docusaurus.config.js`).
- [ ] T032 [P] Implement comprehensive logging for backend services (`backend/src/utils/logger.py`).
- [ ] T033 [P] Refine chatbot responses for clarity and conciseness based on feedback.
- [ ] T034 [P] Add more detailed error handling and user feedback messages.
- [ ] T035 [P] Implement basic unit tests for core backend services (e.g., textbook loading, RAG query processing).
- [ ] T036 [P] Ensure content updates can be processed and indexed within 24 hours (requires research on update strategy).

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately.
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories.
- **User Stories (Phase 3+)**: All depend on Foundational phase completion.
  - User stories can proceed in parallel (if staffed) or sequentially by priority (P1 -> P2 -> P3).
- **Polish (Phase 8)**: Depends on all desired user stories being complete.

### User Story Dependencies

- **US1 (Access Course Content)**: Can start after Foundational (Phase 2). No dependencies on other stories.
- **US2 (RAG Chatbot Queries)**: Can start after Foundational (Phase 2). Depends on US1 for content access.
- **US5 (Selected Text Query)**: Can start after Foundational (Phase 2) and depends on US2 for core chatbot functionality.
- **US3 (Explore Modules)**: Can start after Foundational (Phase 2). May depend on US1 for content display logic.
- **US4 (Hardware Requirements)**: Can start after Foundational (Phase 2). Independent of other stories.

### Within Each User Story Phase

- Tasks marked [P] can be parallelized.
- Core models/services should generally precede endpoints and UI integration.

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel.
- Foundational tasks marked [P] can run in parallel within Phase 2.
- Once Foundational is done, US1, US2, US5, US3, US4 can be worked on in parallel by different team members.
- Within stories with [P] tasks (e.g., US1, US2, US5), parallelize tasks where possible (e.g., model creation vs. backend API logic if they don't directly block each other).

---

## Implementation Strategy

### MVP First (User Story 1)

1.  Complete Phase 1: Setup
2.  Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3.  Complete Phase 3: User Story 1
4.  **STOP and VALIDATE**: Test User Story 1 independently.
5.  Deploy/demo if ready.

### Incremental Delivery

1.  Complete Setup + Foundational → Foundation ready.
2.  Add User Story 1 → Test independently → Deploy/Demo (MVP!).
3.  Add User Story 2 & US5 → Test independently → Deploy/Demo.
4.  Add User Story 3 & US4 → Test independently → Deploy/Demo.
5.  Add Phase 8: Polish tasks.
6.  Each story adds value without breaking previous ones.

### Parallel Team Strategy

With multiple developers:

1.  Team completes Setup + Foundational together.
2.  Once Foundational is done:
    *   Developer A: User Story 1
    *   Developer B: User Story 2 & US5
    *   Developer C: User Story 3 & US4
3.  Stories complete and integrate independently.

---

## TODOs

*   Define specific performance metrics for textbook rendering and chatbot throughput.
*   Finalize choices for RAG libraries, textbook delivery method, and storage solutions after research.
*   Determine exact deployment strategy for FastAPI backend.
*   Clarify any database migration commands.
*   Finalize the `ingest_content.py` script's implementation details.
