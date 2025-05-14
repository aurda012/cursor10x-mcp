[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/aurda012-cursor10x-mcp-badge.png)](https://mseep.ai/app/aurda012-cursor10x-mcp)

![DevContext - The Next Evolution in AI Development Context](https://i.postimg.cc/sghKLKf6/Dev-Context-banner.png)

<div align="center">
  
# 🚀 **Cursor10x is now DevContext** 🚀

### Cursor10x has evolved into DevContext - A more powerful, dedicated context system for developers

<table align="center">
  <tr>
    <td align="center"><b>🧠 Project-Centric</b></td>
    <td align="center"><b>📊 Relationship Graphs</b></td>
    <td align="center"><b>⚡ High Performance</b></td>
  </tr>
  <tr>
    <td align="center">One database per project</td>
    <td align="center">Intelligent code connections</td>
    <td align="center">Minimal resource needs</td>
  </tr>
</table>

### 🔥 **DevContext takes AI development to the next level** 🔥

**🔄 Continuous Context Awareness** - Sophisticated retrieval methods focusing on what matters
**📊 Structured Metadata** - From repository structure down to individual functions
**🧠 Adaptive Learning** - Continuously learns from and adapts to your development patterns
**🤖 Completely Autonomous** - Self-managing context system that works in the background
**📚 External Documentation** - Automatically retrieves and integrates relevant documentation
**📋 Workflow Integration** - Seamless task management workflow built-in

#### 👀 **Be on the lookout** 👀

The DevContext Project Generator is launching in the next couple days and will create a COMPLETE set up for your project to literally 10x your development workflow.

<p align="center">
  <a href="https://github.com/aurda012/devcontext" style="display: inline-block; background-color: rgba(40, 230, 210); color: white; padding: 12px 24px; text-decoration: none; border-radius: 8px; font-weight: bold; box-shadow: 0 4px 6px rgba(0,0,0,0.1); transition: all 0.3s ease;">Visit DevContext Repository</a>
</p>

<i>DevContext is a cutting-edge Model Context Protocol (MCP) server providing developers with continuous, project-centric context awareness that understands your codebase at a deeper level.</i>

</div>

---

## Overview

The Cursor10x Memory System creates a persistent memory layer for AI assistants (specifically Claude), enabling them to retain and recall:

- Recent messages and conversation history
- Active files currently being worked on
- Important project milestones and decisions
- Technical requirements and specifications
- Chronological sequences of actions and events (episodes)
- Code snippets and structures from your codebase
- Semantically similar content based on vector embeddings
- Related code fragments through semantic similarity
- File structures with function and variable relationships

This memory system bridges the gap between stateless AI interactions and continuous development workflows, allowing for more productive and contextually aware assistance.

## System Architecture

The memory system is built on four core components:

1. **MCP Server**: Implements the Model Context Protocol to register tools and process requests
2. **Memory Database**: Uses Turso database for persistent storage across sessions
3. **Memory Subsystems**: Organizes memory into specialized systems with distinct purposes
4. **Vector Embeddings**: Transforms text and code into numerical representations for semantic search

### Memory Types

The system implements four complementary memory types:

1. **Short-Term Memory (STM)**

   - Stores recent messages and active files
   - Provides immediate context for current interactions
   - Automatically prioritizes by recency and importance

2. **Long-Term Memory (LTM)**

   - Stores permanent project information like milestones and decisions
   - Maintains architectural and design context
   - Preserves high-importance information indefinitely

3. **Episodic Memory**

   - Records chronological sequences of events
   - Maintains causal relationships between actions
   - Provides temporal context for project history

4. **Semantic Memory**
   - Stores vector embeddings of messages, files, and code snippets
   - Enables retrieval of content based on semantic similarity
   - Automatically indexes code structures for contextual retrieval
   - Tracks relationships between code components
   - Provides similarity-based search across the codebase

## Features

- **Persistent Context**: Maintains conversation and project context across multiple sessions
- **Importance-Based Storage**: Prioritizes information based on configurable importance levels
- **Multi-Dimensional Memory**: Combines short-term, long-term, episodic, and semantic memory systems
- **Comprehensive Retrieval**: Provides unified context from all memory subsystems
- **Health Monitoring**: Includes built-in diagnostics and status reporting
- **Banner Generation**: Creates informative context banners for conversation starts
- **Database Persistence**: Stores all memory data in Turso database with automatic schema creation
- **Vector Embeddings**: Creates numerical representations of text and code for similarity search
- **Advanced Vector Storage**: Utilizes Turso's F32_BLOB and vector functions for efficient embedding storage
- **ANN Search**: Supports Approximate Nearest Neighbor search for fast similarity matching
- **Code Indexing**: Automatically detects and indexes code structures (functions, classes, variables)
- **Semantic Search**: Finds related content based on meaning rather than exact text matches
- **Relevance Scoring**: Ranks context items by relevance to the current query
- **Code Structure Detection**: Identifies and extracts code components across multiple languages
- **Auto-Embedding Generation**: Automatically creates vector embeddings for indexed content
- **Cross-Reference Retrieval**: Finds related code across different files and components

## Installation

### Prerequisites

- Node.js 18 or higher
- npm or yarn package manager
- Turso database account

### Setup Steps

1. **Configure Turso Database:**

```bash
# Install Turso CLI
curl -sSfL https://get.turso.tech/install.sh | bash

# Login to Turso
turso auth login

# Create a database
turso db create cursor10x-mcp

# Get database URL and token
turso db show cursor10x-mcp --url
turso db tokens create cursor10x-mcp
```

Or you can visit [Turso](https://turso.tech/) and sign up and proceed to create the database and get proper credentials. The free plan will more than cover your project memory.

2. **Configure Cursor MCP:**

Update `.cursor/mcp.json` in your project directory with the database url and turso auth token:

```json
{
  "mcpServers": {
    "cursor10x-mcp": {
      "command": "npx",
      "args": ["cursor10x-mcp"],
      "enabled": true,
      "env": {
        "TURSO_DATABASE_URL": "your-turso-database-url",
        "TURSO_AUTH_TOKEN": "your-turso-auth-token"
      }
    }
  }
}
```

## Tool Documentation

### System Tools

#### `mcp_cursor10x_initConversation`

Initializes a conversation by storing the user message, generating a banner, and retrieving context in one operation. This unified tool replaces the need for separate generateBanner, getComprehensiveContext, and storeUserMessage calls at the beginning of each conversation.

**Parameters:**

- `content` (string, required): Content of the user message
- `importance` (string, optional): Importance level ("low", "medium", "high", "critical"), defaults to "low"
- `metadata` (object, optional): Additional metadata for the message

**Returns:**

- Object with two sections:
  - `display`: Contains the banner to be shown to the user
  - `internal`: Contains the comprehensive context for the agent's use

**Example:**

```javascript
// Initialize a conversation
const result = await mcp_cursor10x_initConversation({
  content: "I need to implement a login system for my app",
  importance: "medium",
});
// Result: {
//   "status": "ok",
//   "display": {
//     "banner": {
//       "status": "ok",
//       "memory_system": "active",
//       "mode": "turso",
//       "message_count": 42,
//       "active_files_count": 3,
//       "last_accessed": "4/15/2023, 2:30:45 PM"
//     }
//   },
//   "internal": {
//     "context": { ... comprehensive context data ... },
//     "messageStored": true,
//     "timestamp": 1681567845123
//   }
// }
```

#### `mcp_cursor10x_endConversation`

Ends a conversation by combining multiple operations in one call: storing the assistant's final message, recording a milestone for what was accomplished, and logging an episode in the episodic memory. This unified tool replaces the need for separate storeAssistantMessage, storeMilestone, and recordEpisode calls at the end of each conversation.

**Parameters:**

- `content` (string, required): Content of the assistant's final message
- `milestone_title` (string, required): Title of the milestone to record
- `milestone_description` (string, required): Description of what was accomplished
- `importance` (string, optional): Importance level ("low", "medium", "high", "critical"), defaults to "medium"
- `metadata` (object, optional): Additional metadata for all records

**Returns:**

- Object with status and results of each operation

**Example:**

```javascript
// End a conversation with finalization steps
const result = await mcp_cursor10x_endConversation({
  content:
    "I've implemented the authentication system with JWT tokens as requested",
  milestone_title: "Authentication Implementation",
  milestone_description:
    "Implemented secure JWT-based authentication with refresh tokens",
  importance: "high",
});
// Result: {
//   "status": "ok",
//   "results": {
//     "assistantMessage": {
//       "stored": true,
//       "timestamp": 1681568500123
//     },
//     "milestone": {
//       "title": "Authentication Implementation",
//       "stored": true,
//       "timestamp": 1681568500123
//     },
//     "episode": {
//       "action": "completion",
//       "stored": true,
//       "timestamp": 1681568500123
//     }
//   }
// }
```

#### `mcp_cursor10x_checkHealth`

Checks the health of the memory system and its database connection.

**Parameters:**

- None required

**Returns:**

- Object with health status and diagnostics

**Example:**

```javascript
// Check memory system health
const health = await mcp_cursor10x_checkHealth({});
// Result: {
//   "status": "ok",
//   "mode": "turso",
//   "message_count": 42,
//   "active_files_count": 3,
//   "current_directory": "/users/project",
//   "timestamp": "2023-04-15T14:30:45.123Z"
// }
```

#### `mcp_cursor10x_getMemoryStats`

Retrieves detailed statistics about the memory system.

**Parameters:**

- None required

**Returns:**

- Object with comprehensive memory statistics

**Example:**

```javascript
// Get memory statistics
const stats = await mcp_cursor10x_getMemoryStats({});
// Result: {
//   "status": "ok",
//   "stats": {
//     "message_count": 42,
//     "active_file_count": 3,
//     "milestone_count": 7,
//     "decision_count": 12,
//     "requirement_count": 15,
//     "episode_count": 87,
//     "oldest_memory": "2023-03-10T09:15:30.284Z",
//     "newest_memory": "2023-04-15T14:30:45.123Z"
//   }
// }
```

#### `mcp_cursor10x_getComprehensiveContext`

Retrieves a unified context from all memory subsystems, combining short-term, long-term, and episodic memory.

**Parameters:**

- None required

**Returns:**

- Object with consolidated context from all memory systems

**Example:**

```javascript
// Get comprehensive context
const context = await mcp_cursor10x_getComprehensiveContext({});
// Result: {
//   "status": "ok",
//   "context": {
//     "shortTerm": {
//       "recentMessages": [...],
//       "activeFiles": [...]
//     },
//     "longTerm": {
//       "milestones": [...],
//       "decisions": [...],
//       "requirements": [...]
//     },
//     "episodic": {
//       "recentEpisodes": [...]
//     },
//     "system": {
//       "healthy": true,
//       "timestamp": "2023-04-15T14:30:45.123Z"
//     }
//   }
// }
```

### Short-Term Memory Tools

#### `mcp_cursor10x_storeUserMessage`

Stores a user message in the short-term memory system.

**Parameters:**

- `content` (string, required): Content of the message
- `importance` (string, optional): Importance level ("low", "medium", "high", "critical"), defaults to "low"
- `metadata` (object, optional): Additional metadata for the message

**Returns:**

- Object with status and timestamp

**Example:**

```javascript
// Store a user message
const result = await mcp_cursor10x_storeUserMessage({
  content: "We need to implement authentication for our API",
  importance: "high",
  metadata: {
    topic: "authentication",
    priority: 1,
  },
});
// Result: {
//   "status": "ok",
//   "timestamp": 1681567845123
// }
```

#### `mcp_cursor10x_storeAssistantMessage`

Stores an assistant message in the short-term memory system.

**Parameters:**

- `content` (string, required): Content of the message
- `importance` (string, optional): Importance level ("low", "medium", "high", "critical"), defaults to "low"
- `metadata` (object, optional): Additional metadata for the message

**Returns:**

- Object with status and timestamp

**Example:**

```javascript
// Store an assistant message
const result = await mcp_cursor10x_storeAssistantMessage({
  content: "I recommend implementing JWT authentication with refresh tokens",
  importance: "medium",
  metadata: {
    topic: "authentication",
    contains_recommendation: true,
  },
});
// Result: {
//   "status": "ok",
//   "timestamp": 1681567870456
// }
```

#### `mcp_cursor10x_trackActiveFile`

Tracks an active file being accessed or modified by the user.

**Parameters:**

- `filename` (string, required): Path to the file being tracked
- `action` (string, required): Action performed on the file (open, edit, close, etc.)
- `metadata` (object, optional): Additional metadata for the tracking event

**Returns:**

- Object with status, filename, action and timestamp

**Example:**

```javascript
// Track an active file
const result = await mcp_cursor10x_trackActiveFile({
  filename: "src/auth/jwt.js",
  action: "edit",
  metadata: {
    changes: "Added refresh token functionality",
  },
});
// Result: {
//   "status": "ok",
//   "filename": "src/auth/jwt.js",
//   "action": "edit",
//   "timestamp": 1681567900789
// }
```

#### `mcp_cursor10x_getRecentMessages`

Retrieves recent messages from the short-term memory.

**Parameters:**

- `limit` (number, optional): Maximum number of messages to retrieve, defaults to 10
- `importance` (string, optional): Filter by importance level

**Returns:**

- Object with status and array of messages

**Example:**

```javascript
// Get recent high importance messages
const messages = await mcp_cursor10x_getRecentMessages({
  limit: 5,
  importance: "high",
});
// Result: {
//   "status": "ok",
//   "messages": [
//     {
//       "id": 42,
//       "role": "user",
//       "content": "We need to implement authentication for our API",
//       "created_at": "2023-04-15T14:30:45.123Z",
//       "importance": "high",
//       "metadata": {"topic": "authentication", "priority": 1}
//     },
//     ...
//   ]
// }
```

#### `mcp_cursor10x_getActiveFiles`

Retrieves active files from the short-term memory.

**Parameters:**

- `limit` (number, optional): Maximum number of files to retrieve, defaults to 10

**Returns:**

- Object with status and array of active files

**Example:**

```javascript
// Get recent active files
const files = await mcp_cursor10x_getActiveFiles({
  limit: 3,
});
// Result: {
//   "status": "ok",
//   "files": [
//     {
//       "id": 15,
//       "filename": "src/auth/jwt.js",
//       "last_accessed": "2023-04-15T14:30:45.123Z",
//       "metadata": {"changes": "Added refresh token functionality"}
//     },
//     ...
//   ]
// }
```

### Long-Term Memory Tools

#### `mcp_cursor10x_storeMilestone`

Stores a project milestone in the long-term memory.

**Parameters:**

- `title` (string, required): Title of the milestone
- `description` (string, required): Description of the milestone
- `importance` (string, optional): Importance level, defaults to "medium"
- `metadata` (object, optional): Additional metadata for the milestone

**Returns:**

- Object with status, title, and timestamp

**Example:**

```javascript
// Store a project milestone
const result = await mcp_cursor10x_storeMilestone({
  title: "Authentication System Implementation",
  description:
    "Implemented JWT authentication with refresh tokens and proper error handling",
  importance: "high",
  metadata: {
    version: "1.0.0",
    files_affected: ["src/auth/jwt.js", "src/middleware/auth.js"],
  },
});
// Result: {
//   "status": "ok",
//   "title": "Authentication System Implementation",
//   "timestamp": 1681568000123
// }
```

#### `mcp_cursor10x_storeDecision`

Stores a project decision in the long-term memory.

**Parameters:**

- `title` (string, required): Title of the decision
- `content` (string, required): Content of the decision
- `reasoning` (string, optional): Reasoning behind the decision
- `importance` (string, optional): Importance level, defaults to "medium"
- `metadata` (object, optional): Additional metadata for the decision

**Returns:**

- Object with status, title, and timestamp

**Example:**

```javascript
// Store a project decision
const result = await mcp_cursor10x_storeDecision({
  title: "JWT for Authentication",
  content: "Use JWT tokens for API authentication with refresh token rotation",
  reasoning:
    "JWTs provide stateless authentication with good security and performance characteristics",
  importance: "high",
  metadata: {
    alternatives_considered: ["Session-based auth", "OAuth2"],
    decision_date: "2023-04-15",
  },
});
// Result: {
//   "status": "ok",
//   "title": "JWT for Authentication",
//   "timestamp": 1681568100456
// }
```

#### `mcp_cursor10x_storeRequirement`

Stores a project requirement in the long-term memory.

**Parameters:**

- `title` (string, required): Title of the requirement
- `content` (string, required): Content of the requirement
- `importance` (string, optional): Importance level, defaults to "medium"
- `metadata` (object, optional): Additional metadata for the requirement

**Returns:**

- Object with status, title, and timestamp

**Example:**

```javascript
// Store a project requirement
const result = await mcp_cursor10x_storeRequirement({
  title: "Secure Authentication",
  content:
    "System must implement secure authentication with password hashing, rate limiting, and token rotation",
  importance: "critical",
  metadata: {
    source: "security audit",
    compliance: ["OWASP Top 10", "GDPR"],
  },
});
// Result: {
//   "status": "ok",
//   "title": "Secure Authentication",
//   "timestamp": 1681568200789
// }
```

### Episodic Memory Tools

#### `mcp_cursor10x_recordEpisode`

Records an episode (action) in the episodic memory.

**Parameters:**

- `actor` (string, required): Actor performing the action (user, assistant, system)
- `action` (string, required): Type of action performed
- `content` (string, required): Content or details of the action
- `importance` (string, optional): Importance level, defaults to "low"
- `context` (string, optional): Context for the episode

**Returns:**

- Object with status, actor, action, and timestamp

**Example:**

```javascript
// Record an episode
const result = await mcp_cursor10x_recordEpisode({
  actor: "assistant",
  action: "implementation",
  content: "Created JWT authentication middleware with token verification",
  importance: "medium",
  context: "authentication",
});
// Result: {
//   "status": "ok",
//   "actor": "assistant",
//   "action": "implementation",
//   "timestamp": 1681568300123
// }
```

#### `mcp_cursor10x_getRecentEpisodes`

Retrieves recent episodes from the episodic memory.

**Parameters:**

- `limit` (number, optional): Maximum number of episodes to retrieve, defaults to 10
- `context` (string, optional): Filter by context

**Returns:**

- Object with status and array of episodes

**Example:**

```javascript
// Get recent episodes in the authentication context
const episodes = await mcp_cursor10x_getRecentEpisodes({
  limit: 5,
  context: "authentication",
});
// Result: {
//   "status": "ok",
//   "episodes": [
//     {
//       "id": 87,
//       "actor": "assistant",
//       "action": "implementation",
//       "content": "Created JWT authentication middleware with token verification",
//       "timestamp": "2023-04-15T14:45:00.123Z",
//       "importance": "medium",
//       "context": "authentication"
//     },
//     ...
//   ]
// }
```

### Vector-Based Memory Tools

#### `mcp_cursor10x_manageVector`

Unified tool for managing vector embeddings with operations for store, search, update, and delete.

**Parameters:**

- `operation` (string, required): Operation to perform ("store", "search", "update", "delete")
- `contentId` (number, optional): ID of the content this vector represents (for store, update, delete)
- `contentType` (string, optional): Type of content ("message", "file", "snippet", etc.)
- `vector` (array, optional): Vector data as array of numbers (for store, update) or query vector (for search)
- `vectorId` (number, optional): ID of the vector to update or delete
- `limit` (number, optional): Maximum number of results for search operation, defaults to 10
- `threshold` (number, optional): Similarity threshold for search operation, defaults to 0.7
- `metadata` (object, optional): Additional info about the vector

**Returns:**

- Object with status and operation results

**Example:**

```javascript
// Store a vector embedding
const result = await mcp_cursor10x_manageVector({
  operation: "store",
  contentId: 42,
  contentType: "message",
  vector: [0.1, 0.2, 0.3, ...], // 128-dimensional vector
  metadata: {
    topic: "authentication",
    language: "en"
  }
});
// Result: {
//   "status": "ok",
//   "operation": "store",
//   "vectorId": 15,
//   "timestamp": 1681570000123
// }

// Search for similar vectors
const searchResult = await mcp_cursor10x_manageVector({
  operation: "search",
  vector: [0.1, 0.2, 0.3, ...], // query vector
  contentType: "snippet", // optional filter
  limit: 5,
  threshold: 0.8
});
// Result: {
//   "status": "ok",
//   "operation": "search",
//   "results": [
//     {
//       "vectorId": 10,
//       "contentId": 30,
//       "contentType": "snippet",
//       "similarity": 0.92,
//       "metadata": { ... }
//     },
//     ...
//   ]
// }
```

## Database Schema

The memory system automatically creates and maintains the following database tables:

- `messages`: Stores user and assistant messages

  - `id`: Unique identifier
  - `timestamp`: Creation timestamp
  - `role`: Message role (user/assistant)
  - `content`: Message content
  - `importance`: Importance level
  - `archived`: Whether the message is archived

- `active_files`: Tracks file activity

  - `id`: Unique identifier
  - `filename`: Path to the file
  - `action`: Last action performed
  - `last_accessed`: Timestamp of last access

- `milestones`: Records project milestones

  - `id`: Unique identifier
  - `title`: Milestone title
  - `description`: Detailed description
  - `timestamp`: Creation timestamp
  - `importance`: Importance level

- `decisions`: Stores project decisions

  - `id`: Unique identifier
  - `title`: Decision title
  - `content`: Decision content
  - `reasoning`: Decision reasoning
  - `timestamp`: Creation timestamp
  - `importance`: Importance level

- `requirements`: Maintains project requirements

  - `id`: Unique identifier
  - `title`: Requirement title
  - `content`: Requirement content
  - `timestamp`: Creation timestamp
  - `importance`: Importance level

- `episodes`: Chronicles actions and events

  - `id`: Unique identifier
  - `timestamp`: Creation timestamp
  - `actor`: Actor performing the action
  - `action`: Type of action
  - `content`: Action details
  - `importance`: Importance level
  - `context`: Action context

- `vectors`: Stores vector embeddings for semantic search

  - `id`: Unique identifier
  - `content_id`: ID of the referenced content
  - `content_type`: Type of content (message, file, snippet)
  - `vector`: Binary representation of the embedding vector
  - `metadata`: Additional metadata for the vector

- `code_files`: Tracks indexed code files

  - `id`: Unique identifier
  - `file_path`: Path to the file
  - `language`: Programming language
  - `last_indexed`: Timestamp of last indexing
  - `metadata`: Additional file metadata

- `code_snippets`: Stores extracted code structures
  - `id`: Unique identifier
  - `file_id`: Reference to the parent file
  - `start_line`: Starting line number
  - `end_line`: Ending line number
  - `symbol_type`: Type of code structure (function, class, variable)
  - `content`: The code snippet content

## Example Workflows

### Optimized Conversation Start

```javascript
// Initialize conversation with a single tool call
// This replaces the need for three separate calls at the start of the conversation
const result = await mcp_cursor10x_initConversation({
  content: "I need help implementing authentication in my React app",
  importance: "high",
});

// Display the banner to the user
console.log("Memory System Status:", result.display.banner);

// Use the context internally (do not show to user)
const context = result.internal.context;
// Use context for more informed assistance
```

### Starting a New Session (Alternative Method)

```javascript
// Generate a memory banner at the start
mcp_cursor10x_generateBanner({});

// Get comprehensive context
mcp_cursor10x_getComprehensiveContext({});

// Store the user message
mcp_cursor10x_storeUserMessage({
  content: "I need help with authentication",
  importance: "high",
});
```

### Tracking User Activity

```javascript
// Track an active file
await mcp_cursor10x_trackActiveFile({
  filename: "src/auth/jwt.js",
  action: "edit",
});
```

## Troubleshooting

### Common Issues

1. **Database Connection Problems**

   - Verify your Turso database URL and authentication token are correct
   - Check network connectivity to the Turso service
   - Verify firewall settings allow the connection

2. **Missing Data**

   - Check that data was stored with appropriate importance level
   - Verify the retrieval query parameters (limit, filters)
   - Check the database health with `mcp_cursor10x_checkHealth()`

3. **Performance Issues**
   - Monitor memory statistics with `mcp_cursor10x_getMemoryStats()`
   - Consider archiving old data if database grows too large
   - Optimize retrieval by using more specific filters

### Diagnostic Steps

1. Check system health:

   ```javascript
   const health = await mcp_cursor10x_checkHealth({});
   console.log("System Health:", health);
   ```

2. Verify memory statistics:

   ```javascript
   const stats = await mcp_cursor10x_getMemoryStats({});
   console.log("Memory Stats:", stats);
   ```

3. Generate a status banner:
   ```javascript
   const banner = await mcp_cursor10x_generateBanner({});
   console.log("Memory Banner:", banner);
   ```

## Importance Levels

When storing items in memory, use appropriate importance levels:

- **low**: General information, routine operations, everyday conversations
- **medium**: Useful context, standard work items, regular features
- **high**: Critical decisions, major features, important architecture elements
- **critical**: Core architecture, security concerns, data integrity issues

## License

MIT
