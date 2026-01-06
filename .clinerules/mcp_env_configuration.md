---
description: Guidelines for managing environment variables and configuration in MCP servers
author: Community
version: 1.0
category: "MCP Development"
tags: ["mcp", "environment", "configuration", "best-practices"]
globs: ["**/*.env", "**/.env.example", "**/mcp-server/**/*"]
---

# Environment Configuration in MCP Servers

## Overview
Model Context Protocol (MCP) servers often require access to API keys and configuration values that should not be committed to version control. This document outlines the recommended approach for managing environment variables in MCP servers.

## Recommended Implementation

### 1. Project Structure
Place your `.env` file in the root directory of your MCP server project:

```
your-mcp-server/
├── .env              # Environment variables (not committed to git)
├── .env.example      # Example template (committed to git)
├── package.json
└── src/
    └── ...
```

### 2. Path Resolution
When loading the `.env` file, use a reliable path resolution method that works both in development and production:

```typescript
import * as dotenv from 'dotenv';
import { fileURLToPath } from 'url';
import { dirname, resolve } from 'path';
import * as fs from 'fs';

// Get the directory path for loading the .env file
const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);
const rootDir = resolve(__dirname, '../..'); // Adjust based on file location

// Load environment variables from .env file
dotenv.config({ path: resolve(rootDir, '.env') });

// Validate the configuration
if (fs.existsSync(resolve(rootDir, '.env'))) {
  console.debug('Environment file loaded successfully');
} else {
  console.warn('No .env file found at', resolve(rootDir, '.env'));
}
```

### 3. Variable Access
Use a helper function to safely access required environment variables:

```typescript
const getRequiredEnv = (key: string): string => {
  const value = process.env[key];
  if (!value) {
    throw new Error(`${key} environment variable is required. Please set it in your configuration.`);
  }
  return value;
};

// Usage
const apiKey = getRequiredEnv('API_KEY');
```

### 4. MCP Server Configuration
When configuring the MCP server in a desktop application like Claude Desktop, provide the environment variables directly:

```json
{
  "mcpServers": {
    "your-mcp-server": {
      "command": "/path/to/your-mcp-server/build/index.js",
      "env": {
        "API_KEY": "your-api-key-here",
        "OTHER_CONFIG": "other-value"
      }
    }
  }
}
```

## Common Issues

### Path Resolution
- **Issue**: The `.env` file can't be found at runtime
- **Solution**: Ensure the path is correctly calculated relative to the file location
- **Debugging**: Add path logging to verify the correct paths are being used

### ES Modules vs CommonJS
- **Issue**: `require('fs')` not working in ES modules
- **Solution**: Use `import * as fs from 'fs'` with ES modules
- **Verification**: Check your `package.json` for `"type": "module"`

### Environment Precedence
Environment variables from the system take precedence over those in the `.env` file. When debugging, check both sources.

## Best Practices

1. **Never commit** `.env` files to version control
2. **Always provide** an `.env.example` template
3. **Validate** required environment variables at startup
4. **Use path resolution** that works in all environments
5. **Document** all required environment variables in your README
