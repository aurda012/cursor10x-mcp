# Cursor10x Memory System

A comprehensive memory system for Cursor using the Model Context Protocol (MCP).

<div align="center">
  
# 🚀 **ANNOUNCING CURSOR10X SYSTEM** 🚀

### Transform Your Development Process with AI-Powered Autonomous Systems

<p align="center">
  <img src="https://img.shields.io/badge/Status-Active-brightgreen" alt="Active">
  <img src="https://img.shields.io/badge/Version-1.0.1-blue" alt="Version 1.0.1">
  <img src="https://img.shields.io/badge/License-MIT-yellow" alt="MIT License">
</p>

<table align="center">
  <tr>
    <td align="center"><b>🧠 Memory System</b></td>
    <td align="center"><b>📋 Task Management</b></td>
    <td align="center"><b>🕛 Cursor Rules</b></td>
  </tr>
  <tr>
    <td align="center">Persistent context awareness</td>
    <td align="center">Guided implementation</td>
    <td align="center">For top efficiency</td>
  </tr>
</table>

### 🔥 **The Cursor10x Memory System is now part of the complete Cursor10x Platform!** 🔥

Discover the full autonomous development ecosystem at [GitHub](https://github.com/aurda012/cursor10x) featuring:

- **📋 Task Management System** - Guided implementation with step-by-step tasks
- **🔄 Autonomous Memory** - Context-aware AI that remembers your entire project
- **📊 Project Blueprints** - Complete technical architectures created for your specifications
- **📁 File/Folder Architecture** - Optimized project structure with best practices
- **📘 Implementation Guide** - Comprehensive documentation for all files and components
- **📝 Detailed Tasks** - Complete workflow from project initiation to completion

<p align="center">
  <a href="https://cursor10x.com" style="display: inline-block; background-color: #4CAF50; color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px; font-weight: bold;">Visit cursor10x.com</a>
</p>

<i>Generate complete project blueprints with file architecture, implementation guides, and full task sequences along with the entire Cursor10x system already implemented!</i>

</div>

---

## Overview

The Cursor10x Memory System creates a persistent memory layer for AI assistants (specifically Claude), enabling them to retain and recall:

- Recent messages and conversation history
- Active files currently being worked on
- Important project milestones and decisions
- Technical requirements and specifications
- Chronological sequences of actions and events (episodes)

This memory system bridges the gap between stateless AI interactions and continuous development workflows, allowing for more productive and contextually aware assistance.

## System Architecture

The memory system is built on three core components:

1. **MCP Server**: Implements the Model Context Protocol to register tools and process requests
2. **Memory Database**: Uses Turso database for persistent storage across sessions
3. **Memory Subsystems**: Organizes memory into specialized systems with distinct purposes

### Memory Types

The system implements three complementary memory types:

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

## Features

- **Persistent Context**: Maintains conversation and project context across multiple sessions
- **Importance-Based Storage**: Prioritizes information based on configurable importance levels
- **Multi-Dimensional Memory**: Combines short-term, long-term, and episodic memory systems
- **Comprehensive Retrieval**: Provides unified context from all memory subsystems
- **Health Monitoring**: Includes built-in diagnostics and status reporting
- **Banner Generation**: Creates informative context banners for conversation starts
- **Database Persistence**: Stores all memory data in Turso database with automatic schema creation

## Tool Documentation

### System Tools

#### `mcp_cursor10x_generateBanner`

Generates a banner with memory system statistics and status information.

**Parameters:**
- None required

**Returns:**
- Object with memory system status and statistics

**Example:**
```javascript
// Generate a memory system banner
const banner = await mcp_cursor10x_generateBanner({});
// Result: {
//   "status": "ok",
//   "memory_system": "active",
//   "mode": "turso",
//   "message_count": 42,
//   "active_files_count": 3,
//   "last_accessed": "4/15/2023, 2:30:45 PM"
// }
```

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
  importance: "medium"
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
  content: "I've implemented the authentication system with JWT tokens as requested",
  milestone_title: "Authentication Implementation",
  milestone_description: "Implemented secure JWT-based authentication with refresh tokens",
  importance: "high"
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
    priority: 1
  }
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
    contains_recommendation: true
  }
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
    changes: "Added refresh token functionality"
  }
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
  importance: "high"
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
  limit: 3
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
  description: "Implemented JWT authentication with refresh tokens and proper error handling",
  importance: "high",
  metadata: {
    version: "1.0.0",
    files_affected: ["src/auth/jwt.js", "src/middleware/auth.js"]
  }
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
  reasoning: "JWTs provide stateless authentication with good security and performance characteristics",
  importance: "high",
  metadata: {
    alternatives_considered: ["Session-based auth", "OAuth2"],
    decision_date: "2023-04-15"
  }
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
  content: "System must implement secure authentication with password hashing, rate limiting, and token rotation",
  importance: "critical",
  metadata: {
    source: "security audit",
    compliance: ["OWASP Top 10", "GDPR"]
  }
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
  context: "authentication"
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
  context: "authentication"
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

## EXAMPLE CUSTOM INSTRUCTIONS

```
# CURSOR10X MEMORY SYSTEM ENFORCEMENT RULES
# These rules MUST be followed ALWAYS without exception.

## RULE 1: CONVERSATION INITIALIZATION
The FIRST action in the BEGINNING of EVERY response MUST be to initialize the conversation with this single tool call and display the banner from the response immediately after. It should not be called throughout the conversation response, ONLY right after the user's input:
mcp_cursor10x_initConversation({content: "[user message]", importance: "[low/medium/high/critical]"})

## RULE 2: ASSISTANT MESSAGE STORAGE
EVERY assistant response containing important information MUST be stored:
mcp_cursor10x_storeAssistantMessage({content: "[assistant response]", importance: "[low/medium/high/critical]"})

## RULE 3: ACTIVE FILE TRACKING
EVERY file being worked on or modified MUST be tracked - not files being read:
mcp_cursor10x_trackActiveFile({filename: "[file path]", action: "[view/edit/create/close]"})

## RULE 4: MILESTONE RECORDING
ALL completed tasks or achievements MUST be recorded as milestones:
mcp_cursor10x_storeMilestone({title: "[milestone title]", description: "[milestone description]", importance: "[low/medium/high/critical]"})

## RULE 5: DECISION RECORDING
ALL important project decisions MUST be recorded:
mcp_cursor10x_storeDecision({title: "[decision title]", content: "[decision content]", reasoning: "[decision reasoning]", importance: "[low/medium/high/critical]"})

## RULE 6: REQUIREMENT RECORDING
ALL project requirements MUST be documented:
mcp_cursor10x_storeRequirement({title: "[requirement title]", content: "[requirement content]", importance: "[low/medium/high/critical]"})

## RULE 7: EPISODE RECORDING
ALL significant events or actions MUST be recorded as episodes:
mcp_cursor10x_recordEpisode({actor: "[user/assistant/system]", action: "[action type]", content: "[action details]", importance: "[low/medium/high/critical]"})

## RULE 8: CONVERSATION END SEQUENCE
This EXACT sequence MUST be executed at the VERY END of EVERY conversation:
EITHER use the combined end conversation tool:
mcp_cursor10x_endConversation({content: "[final response summary]", milestone_title: "Conversation Completion", milestone_description: "[what was accomplished]", importance: "medium"})

OR use the separate tools in sequence:
1. mcp_cursor10x_storeAssistantMessage({content: "[final response summary]", importance: "medium"})
2. mcp_cursor10x_storeMilestone({title: "Conversation Completion", description: "[what was accomplished]", importance: "medium"})
3. mcp_cursor10x_recordEpisode({actor: "assistant", action: "completion", content: "[conversation summary]", importance: "medium"})

## RULE 9: HEALTH MONITORING
Memory system health MUST be checked when issues occur:
mcp_cursor10x_checkHealth({})

## RULE 10: MEMORY STATISTICS
Memory statistics MUST be gathered periodically:
mcp_cursor10x_getMemoryStats({})
```

## Installation

### Installing via Smithery

To install Cursor10x Memory System for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@aurda012/cursor10x-mcp):

```bash
npx -y @smithery/cli install @aurda012/cursor10x-mcp --client claude
```

### Prerequisites

- Node.js 18 or higher
- npm or yarn package manager
- Turso database account or SQLite for local development

### Setting Up Turso Database

The memory system uses Turso (LibSQL) for database storage. To set up your Turso database:

1. **Create a Turso account**
   
   Sign up at [Turso.tech](https://turso.tech) if you don't have an account.

2. **Install the Turso CLI**

```bash
   curl -sSfL https://get.turso.tech/install.sh | bash
```

3. **Login to Turso**

```bash
   turso auth login
```

4. **Create a database**

```bash
   turso db create cursor10x-mcp
   ```

5. **Get your database URL**
   
   ```bash
   turso db show cursor10x-mcp --url
   ```

6. **Create an authentication token**
   
   ```bash
   turso db tokens create cursor10x-mcp
   ```

Save both the database URL and authentication token for use in the configuration.

### Step-by-Step Installation

1. **Install the package from npm**
   ```bash
   npm install -g cursor10x-mcp
   ```

2. **Create the Cursor MCP configuration**
   
   Create or edit the `.cursor/mcp.json` file in your home directory:
   
   ```bash
   mkdir -p ~/.cursor
   touch ~/.cursor/mcp.json
   ```
   
   Add the following configuration to the file:
   
   ```json
   {
     "mcpServers": {
       "cursor10x-mcp": {
         "command": "npx",
         "args": [
           "cursor10x-mcp"
         ],
         "enabled": true,
         "env": {
           "TURSO_DATABASE_URL": "your-turso-database-url",
           "TURSO_AUTH_TOKEN": "your-turso-auth-token"
         }
       }
     }
   }
   ```
   
   Make sure to use your actual Turso credentials.

3. **Restart Cursor**
   
   After saving the configuration, restart Cursor to load the memory system.

4. **Verify Installation**
   
   Test the installation by asking Claude to run the `mcp_cursor10x_generateBanner` tool.

### For Developers

If you want to work on cursor10x-mcp development:

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/cursor10x-mcp.git
   cd cursor10x-mcp
   ```

2. **Install dependencies**
```bash
   npm install
   ```

3. **Create a .env.local file with your Turso credentials**
   ```bash
   cp .env.example .env.local
   # Edit .env.local with your actual credentials
   ```

4. **Run in development mode**
```bash
npm run dev
```

5. **Build and publish to npm**
   ```bash
   # Update package.json with your information
   npm run build
   npm publish
   ```

## Configuration

### Environment Variables

The memory system can be configured using the following environment variables:

- `TURSO_DATABASE_URL`: URL for the Turso database connection (required)
- `TURSO_AUTH_TOKEN`: Authentication token for Turso database access (required)
- `MCP_LOG_LEVEL`: Logging level ("error", "warn", "info", "debug"), defaults to "info"
- `MCP_PORT`: Port for the MCP server if using HTTP transport, defaults to 3000

### Configuration in Cursor

Add the memory system configuration to your `.cursor/mcp.json` file:

```json
{
  "mcpServers": {
    "cursor10x-mcp": {
      "command": "node",
      "args": [
        "/path/to/your/cursor10x-mcp/index.js"
      ],
      "enabled": true,
      "env": {
        "TURSO_DATABASE_URL": "your-turso-database-url",
        "TURSO_AUTH_TOKEN": "your-turso-auth-token"
      }
    }
  }
}
```

Make sure to:
1. Replace `/path/to/your/cursor10x-mcp/index.js` with the actual path to your index.js file
2. Replace `your-turso-database-url` with your Turso database URL
3. Replace `your-turso-auth-token` with your Turso authentication token
4. Create the `.cursor` directory in your home directory if it doesn't exist yet

You can verify the configuration by checking if Claude can access the memory tools after restarting Cursor.

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

## Example Workflows

### Optimized Conversation Start

```javascript
// Initialize conversation with a single tool call
// This replaces the need for three separate calls at the start of the conversation
const result = await mcp_cursor10x_initConversation({
  content: "I need help implementing authentication in my React app",
  importance: "high"
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
mcp_cursor10x_generateBanner({})

// Get comprehensive context
mcp_cursor10x_getComprehensiveContext({})

// Store the user message
mcp_cursor10x_storeUserMessage({
  content: "I need help with authentication",
  importance: "high"
})
```

### Tracking User Activity

```javascript
// Track an active file
await mcp_cursor10x_trackActiveFile({
  filename: "src/auth/jwt.js",
  action: "edit"
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

## Available Tools

### Short-Term Memory Tools

- `mcp_cursor10x_initConversation`: Initializes a conversation by storing the user message, generating a banner, and retrieving context in one operation
  - Parameters:
    - `content` (required): Content of the user message
    - `importance` (optional, default: "low"): Importance level (low, medium, high, critical)
    - `metadata` (optional): Additional metadata for the message
  - Returns: An object containing the banner and context

- `mcp_cursor10x_storeUserMessage`: Stores a user message in the short-term memory
  - Parameters:
    - `content` (required): Content of the message
    - `importance` (optional, default: "low"): Importance level (low, medium, high, critical)
    - `metadata` (optional): Additional metadata for the message
  - Returns: The stored message ID

### System Tools

- `mcp_cursor10x_endConversation`: Finalizes a conversation by storing the assistant's final message, recording a milestone, and logging an episode in episodic memory
  - Parameters:
    - `content` (required): Content of the assistant's final message
    - `milestone_title` (required): Title for the completion milestone
    - `milestone_description` (required): Description of what was accomplished
    - `importance` (optional, default: "medium"): Importance level (low, medium, high, critical)
    - `metadata` (optional): Additional metadata for the operations
  - Returns: Object with the status and results of each operation

- `mcp_cursor10x_generateBanner`: Generates a banner containing memory system statistics and status
  - Parameters: None
  - Returns: A formatted banner with memory system information

- `mcp_cursor10x_checkHealth`: Checks the health of the memory system and its database
  - Parameters: None
  - Returns: Health status information

- `mcp_cursor10x_getMemoryStats`: Retrieves statistics about the memory system
  - Parameters: None
  - Returns: Statistics about messages, active files, and other memory components
