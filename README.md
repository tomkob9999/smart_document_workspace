# Smart Document Workspace

Smart Document Workspace is a client-side document platform designed to enhance how users interact with their files. It uses Retrieval-Augmented Generation (RAG) technology to provide contextual AI-assisted answers based on your own documents — all processed locally in the browser for better privacy.

This tool is useful for researchers, business professionals, and students who need fast, context-aware access to their materials without relying on external servers.

---

## Features

### Document Management

* **Multiple Workspaces:** Organize content by project or topic.
* **Drag-and-Drop Upload:** Supports TXT, PDF, DOC, DOCX, and MD formats.
* **Instant Processing:** Documents are vectorized in real-time.
* **Organized Library:** Displays uploaded documents with relevant metadata.

### AI Integration

* **Model Selection:** Choose between GPT-3.5-turbo or GPT-4 for each workspace.
* **Contextual Answers:** Responses are grounded in your own content.
* **Semantic Search:** Use natural language to search across your library.
* **Conversation History:** Retains multi-turn context within rooms.

### Privacy and Local Processing

* **Browser-Based:** All document parsing is done on the client side.
* **No Uploads Required:** Files stay local except when calling external APIs (e.g., OpenAI).
* **Offline Mode:** Core functionality is available without internet access.
* **Local Storage:** Uses IndexedDB for persistence.

### Usability

* **Clean Interface:** Simplified layout optimized for productivity.
* **Responsive Design:** Works across desktop and mobile.
* **User Feedback:** Progress bars and notifications for user actions.
* **Custom Settings:** Adjust API keys and model preferences.

---

## Technical Overview

### Components

* **ClientStorage:** Manages all persistent data using IndexedDB.
* **VectorSearchEngine:** Performs semantic search using Transformers.js and MiniLM model.
* **ClientSideRAGApp:** Coordinates UI state, search, and language model interactions.

### Tech Stack

* **Frontend:** Vanilla JavaScript with ES6 modules
* **Embeddings:** Xenova/Transformers.js
* **Storage:** IndexedDB
* **Styling:** TailwindCSS
* **Icons:** FontAwesome
* **API Integration:** OpenAI API

### Data Flow

1. **Upload Files** → Read and extract text locally
2. **Generate Embeddings** → Convert text to vectors
3. **Store Locally** → Save files and vectors to IndexedDB
4. **Ask Questions** → Convert questions to vectors
5. **Retrieve Context** → Match vectors to relevant text
6. **Generate Answer** → Send context and query to OpenAI

### Security Model

All core processing happens in-browser. Only user queries and context snippets are sent to external APIs, minimizing exposure of document data.

---

## Getting Started

### Basic Usage

1. Open the app in your browser and configure your OpenAI API key in settings.
2. Create a workspace for your project.
3. Select the workspace (room) and upload documents.
4. Click “Process Documents” to enable querying.
5. Ask questions in the chat input — answers will reflect your uploaded documents.

### Advanced Options

* Maintain multiple rooms with separate documents and histories.
* Change models (e.g., GPT-3.5 or GPT-4) based on task needs.
* Reset conversations using the “Clear History” button.
* Configure API and model settings from the settings panel.

### Best Practices

* Group related documents for more relevant responses.
* Ask targeted, document-related questions.
* Use GPT-3.5 for speed; GPT-4 for detailed answers.
* Be aware that only small query snippets go to OpenAI — documents remain local.

---

## Roadmap

### Known Issues

* **Room Switching Bug:** Vector context may not restore correctly when switching rooms. Fix in progress.

### Planned Features

* Support for Office files like PowerPoint and Excel
* Highlighted full-text search
* Export chats and summaries
* Shared rooms for collaboration
* Custom local AI and embedding models
* Document annotations
* Analytics and usage stats

### Technical Enhancements

* Performance improvements for large files
* Better mobile UI
* Full offline capability
* Progressive Web App (PWA) support
* Backup and restore features
* International language support

### AI Roadmap

* Hierarchical and multi-hop retrieval
* Auto-summarization of documents
* Document clustering
* Improved citation formatting
* Smart query suggestions

© 2025 Tomio Kobayashi

© 2025 Tomio Kobayashi

---

Let me know if you want a downloadable `.md` version or if you'd like to adjust the tone even further (e.g., more technical, more instructional, etc.).
