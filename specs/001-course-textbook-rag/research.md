# Research for Physical AI & Humanoid Robotics Course Textbook with RAG Chatbot

**Feature Branch**: `001-course-textbook-rag`  
**Created**: 2026-04-18  
**Purpose**: Resolve remaining unknowns and gather best practices for the implementation plan.

## Research Tasks and Findings

### 1. Performance Metrics Definition

**Task**: Define specific performance metrics for textbook rendering (pages/sec) and chatbot interaction (queries/sec) based on typical educational use cases.

**Findings**: For textbook rendering, a good target is under 500ms per page. For chatbot interaction, aim for 10-20 queries per second per instance.

**Decision**: Textbook rendering: < 500ms per page. Chatbot query throughput: 10 queries/second/instance.

**Rationale**: Balances user experience with realistic technical capabilities.

**Alternatives Considered**: Higher rendering speeds (increased complexity), lower query throughput (impacts user experience in high-demand scenarios).

---

### 2. Web Integration Best Practices

**Task**: Investigate best practices for integrating FastAPI (for RAG chatbot) with Docusaurus (for textbook delivery), focusing on user experience and data flow.

**Findings**: Data Flow: Docusaurus frontend makes HTTP requests to FastAPI backend. Communication: Standard RESTful API calls. CORS: FastAPI needs proper configuration. Deployment: Separate deployments for Docusaurus (GitHub Pages) and FastAPI (e.g., Render, Vercel). User Experience: Asynchronous calls for chatbot, clear loading states.

**Decision**: Implement RESTful API calls from Docusaurus to FastAPI with appropriate CORS configuration and separate deployments.

**Rationale**: Standard and robust integration pattern, offering flexibility and scalability.

**Alternatives Considered**: Embedding chatbot directly in Docusaurus (not feasible), monolithic framework (overkill).

---
