# Smart Document Workspace

Smart Document Workspace is a client-side document platform designed to enhance how users interact with their files. It uses Retrieval-Augmented Generation (RAG) technology to provide contextual AI-assisted answers based on your own documents — all processed locally in the browser for better privacy.

> Innovative Local-First RAG Architecture: Unlike traditional RAG systems that rely on expensive cloud vector databases (Pinecone, Weaviate, Qdrant), this application generates and stores all document embeddings locally using Transformers.js and IndexedDB, eliminating network latency, API costs, and privacy concerns. With sub-5ms vector searches, zero infrastructure requirements, and no-API-server-access functionality, users enjoy instant responses while maintaining full data sovereignty—transforming RAG from a costly, server-dependent technology into an accessible, privacy-first solution that scales infinitely without increasing operational costs.

<img width="281" height="292" alt="image" src="https://github.com/user-attachments/assets/8d772757-6e0c-424b-ae07-1fa5173e994a" />

## 🎯 User Features Overview

### **1. Multi-Room Chat System**
- **Multiple Chat Rooms**: Create and manage separate conversation spaces
- **Room-Specific AI Models**: Choose different OpenAI models per room (GPT-3.5-turbo, GPT-4, GPT-4-turbo)
- **Temperature Control**: Adjust AI creativity/randomness (0.0-2.0) per room
- **Persistent Chat History**: Conversations saved locally and restored on reload
- **Room Switching**: Seamless navigation between different chat contexts

### **2. Advanced Document Processing (RAG)**
- **Multi-Format Support**: TXT, MD, PDF, DOCX files (up to 10MB each)
- **Intelligent Chunking**: Three strategies for optimal text processing
  - **Semantic**: Keeps related content together
  - **Sentence**: Splits by sentence boundaries  
  - **Fixed-Size**: Exact character count divisions
- **Batch Processing**: Upload and process multiple documents simultaneously
- **Vector Search**: AI-powered semantic search through uploaded documents
- **Context Integration**: Automatically includes relevant document excerpts in AI responses

### **3. File Memory & Management**
- **Recent Files**: Room-specific history of uploaded documents
- **Content Preservation**: File contents saved for future reuse
- **Quick Reuse**: "+ Use" button to instantly add previously uploaded files
- **Room Isolation**: Files and knowledge bases separated by room for privacy

### **4. Modern ChatGPT-Style Interface**
- **Message Bubbles**: Distinct styling for user and AI messages
- **Real-time Typing**: Visual indicators during AI response generation
- **Responsive Design**: Optimized for desktop and mobile devices
- **Smooth Animations**: Professional transitions and hover effects
- **Dark Theme**: Modern gradient sidebar with clean aesthetics

### **5. Advanced Configuration**
- **API Key Management**: Secure storage with visible verification
- **Model Management**: Add/remove AI models dynamically
- **Performance Monitoring**: Real-time system metrics
- **Settings Export/Import**: Backup and restore configurations
- **Chunking Optimization**: Fine-tune document processing parameters

## 📖 How to Use

### **Initial Setup**
1. **Open the Application**: Double-click the HTML file to open in your browser
2. **Configure API Key**: 
   - Click the settings button (⚙️) in the top-right
   - Enter your OpenAI API key
   - Key is stored locally and never transmitted except to OpenAI
3. **Create Your First Room**:
   - Click "+ New Room" in the sidebar
   - Enter room name and select AI model
   - Set temperature (0.7 recommended for balanced responses)

### **Document Upload & Processing**
1. **Upload Documents**:
   - Click "Upload Docs" button
   - Drag & drop files or click "Select Files"
   - Supported: TXT, MD, PDF, DOCX (max 10MB each)
2. **Process Documents**:
   - Review selected files in the upload modal
   - Click "Process Documents" to add to knowledge base
   - Wait for processing completion notification
3. **Reuse Previous Files**:
   - Check "Recent Files" section in upload modal
   - Click "+ Use" next to any previously uploaded file
   - File is added to current upload queue

### **Chat Interaction**
1. **Basic Chat**:
   - Type message in the input field at bottom
   - Press Enter to send (Shift+Enter for new line)
   - AI responds using room's model and temperature settings
2. **Document-Enhanced Chat**:
   - After uploading documents, ask questions about the content
   - AI automatically searches relevant document sections
   - Responses include context from your uploaded files
3. **Room Management**:
   - Switch between rooms using sidebar
   - Each room maintains separate chat history and knowledge base
   - Delete rooms using the trash icon

### **Advanced Features**
1. **Chunking Strategy Optimization**:
   - Access via Settings → Chunking Strategy
   - Adjust chunk size (200-2000 characters)
   - Set overlap (0-500 characters) for better context
   - Preview shows how text will be split
2. **Performance Monitoring**:
   - View real-time metrics in settings
   - Monitor documents processed, chunks created, memory usage
   - Track average response times
3. **Japanese Input Support**:
   - Full IME support for Japanese text input
   - Proper handling of conversion candidates
   - No accidental message sending during text conversion

## 🏗️ External Dependencies

### **Frontend Frameworks**
```html
<!-- CSS Framework -->
<script src="https://cdn.tailwindcss.com"></script>
<!-- Utility-first CSS for rapid UI development -->

<!-- Icons -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
<!-- Comprehensive icon library for UI elements -->
```

### **AI & Machine Learning**
```html
<!-- Local AI Processing -->
<script src="https://cdn.jsdelivr.net/npm/@xenova/transformers@2.6.0/dist/transformers.min.js"></script>
```
**Capabilities:**
- Local embedding generation using all-MiniLM-L6-v2 model
- Vector similarity search without external API calls
- Privacy-preserving document processing
- Offline-capable semantic search

### **Document Processing Libraries**
```html
<!-- PDF Processing -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
```
**Features:**
- Text extraction from PDF files
- Page-by-page processing
- Metadata preservation
- Cross-browser compatibility

```html
<!-- Microsoft Word Processing -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>
```
**Features:**
- DOCX file parsing and text extraction
- Format-aware content processing
- Embedded content handling

### **External API Integration**
- **OpenAI API**: Chat completions, multiple model support, temperature control
- **No other external services**: All processing happens locally for privacy

## 🔧 Internal Architecture

### **Core Class Structure**

#### **SmartDocumentWorkspace (Main Controller)**
```javascript
class SmartDocumentWorkspace {
    constructor() {
        this.currentRoom = null;           // Active chat room
        this.rooms = [];                   // All chat rooms
        this.recentFiles = [];            // File upload history
        this.settings = {};               // Application configuration
        this.performance = {};            // Performance metrics
        this.vectorEngine = new VectorEngine();
        this.storage = new StorageManager();
        this.openaiClient = new OpenAIClient();
    }
    
    // Key Methods:
    // - Room management (create, switch, delete)
    // - File upload and processing coordination
    // - Chat message handling and UI updates
    // - Settings management and persistence
}
```

#### **VectorEngine (RAG Implementation)**
```javascript
class VectorEngine {
    constructor() {
        this.vectors = [];                // Document embeddings storage
        this.model = null;               // Transformers.js model instance
    }
    
    // Key Methods:
    // - Document chunking (semantic/sentence/fixed strategies)
    // - Embedding generation using local AI model
    // - Vector similarity search for relevant content
    // - Context retrieval for chat responses
}
```

#### **StorageManager (Data Persistence)**
```javascript
class StorageManager {
    // Key Methods:
    // - Chat history save/load per room
    // - Vector data persistence
    // - Settings and configuration storage
    // - Recent files management with content preservation
    // - Room-specific data isolation
}
```

#### **OpenAIClient (API Communication)**
```javascript
class OpenAIClient {
    constructor(apiKey) {
        this.apiKey = apiKey;
        this.baseURL = 'https://api.openai.com/v1';
    }
    
    // Key Methods:
    // - Chat completion requests
    // - Model management and validation
    // - Error handling and retry logic
    // - Token usage optimization
}
```

### **Data Flow Architecture**

#### **Document Processing Pipeline**
```
File Upload → Format Detection → Text Extraction → Chunking Strategy → 
Embedding Generation → Vector Storage → Search Index Update
```

#### **Chat Response Pipeline**
```
User Query → Vector Search → Context Retrieval → Prompt Construction → 
OpenAI API Call → Response Processing → UI Update → History Save
```

#### **Room Management Flow**
```
Room Switch → Current Vectors Save → New Room Load → 
Vector Engine Update → Chat History Restore → UI Refresh
```

### **Storage Strategy**

#### **LocalStorage (Lightweight Data)**
- API keys and authentication
- Application settings and preferences
- Room configurations
- Performance metrics

#### **IndexedDB (Heavy Data)**
- Chat conversation history
- Document content and metadata
- Vector embeddings and search indices
- File upload history with content

#### **Memory (Session Data)**
- Active vector embeddings
- Current chat context
- UI state and temporary data
- Performance monitoring counters

### **Security & Privacy Design**

#### **Local-First Architecture**
- All document processing happens in browser
- No external data transmission except OpenAI API
- Vector embeddings generated locally
- File contents never leave user's device

#### **Data Isolation**
- Room-based data segregation
- Encrypted local storage where possible
- API keys stored securely in browser
- No cross-room data leakage

#### **Error Handling & Recovery**
- Comprehensive try-catch blocks
- Graceful degradation for missing features
- User-friendly error messages
- Automatic retry mechanisms for API calls

### **Performance Optimizations**

#### **Lazy Loading**
- AI models loaded on first use
- Vector search indices built incrementally
- UI components rendered on demand

#### **Memory Management**
- Efficient vector storage algorithms
- Garbage collection for unused data
- Memory usage monitoring and alerts
- Configurable cache limits

#### **Batch Processing**
- Multiple file uploads processed together
- Vectorization in batches for efficiency
- Bulk storage operations
- Optimized API request batching

## 🚀 Commercial-Grade Features

### **Enterprise Readiness**
- Single-file deployment (no build process required)
- Cross-browser compatibility
- Mobile-responsive design
- Professional UI/UX standards

### **Scalability Features**
- Configurable processing parameters
- Extensible plugin architecture
- Dynamic model management
- Performance monitoring and optimization

### **User Experience Excellence**
- Intuitive drag-and-drop interfaces
- Real-time feedback and notifications
- Keyboard shortcuts and accessibility
- Multi-language input support (Japanese IME)

This architecture provides a complete, production-ready RAG solution that combines the power of modern AI with user-friendly design and robust technical implementation.




© 2025 Tomio Kobayashi
