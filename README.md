# n8n Workflow Builder MCP Server

This project provides an MCP server for managing n8n workflows. It allows you to create, update, delete, activate, and deactivate workflows through a set of tools available in the Claude App.

**Important:**  
This version only supports **npm** for package management and server execution.

## Requirements

- Node.js (v14+ recommended)
- npm
- Claude App for integration capabilities

## Installation Guide

### 1. Clone the Repository

Clone the repository from GitHub:

```bash
git clone https://github.com/salacoste/n8n-workflow-builder.git
```

Then navigate to the project directory:

```bash
cd n8n-workflow-builder
```

### 2. Install Dependencies

Install the necessary dependencies using npm:

```bash
npm install
```

### 3. Configure Environment Variables

Create an `.env` file in the project root with the following variables:

```
N8N_HOST=https://your-n8n-instance.com/api/v1/
N8N_API_KEY=your_api_key_here
```

### 4. Build and Run

Use the following commands to build and run the project:

- **Build the project:**
  
  ```bash
  npm run build
  ```

- **Start the MCP Server:**
  
  ```bash
  npm start
  ```

The server will start and accept requests via stdio.

### 5. Claude App Integration

For integration with Claude App, you need to create a configuration file `cline_mcp_settings.json`. You can copy the example from `cline_mcp_settings.example.json` and edit it:

```bash
cp cline_mcp_settings.example.json cline_mcp_settings.json
```

Then edit the file, providing the correct environment variable values:

```json
{
  "n8n-workflow-builder": {
    "command": "node",
    "args": ["path/to/your/project/build/index.js"],
    "env": {
      "N8N_HOST": "https://your-n8n-instance.com/api/v1/",
      "N8N_API_KEY": "your_api_key_here"
    },
    "disabled": false,
    "alwaysAllow": [
      "list_workflows",
      "get_workflow",
      "list_executions",
      "get_execution"
    ],
    "autoApprove": [
      "create_workflow",
      "update_workflow",
      "activate_workflow",
      "deactivate_workflow",
      "delete_workflow",
      "delete_execution"
    ]
  }
}
```

**Important:** Do not add `cline_mcp_settings.json` to the repository as it contains your personal access credentials.

## Available Tools

### MCP Tools

The following tools are defined in the server and can be accessed through Claude App:

#### Workflow Management
- **list_workflows**: Displays a list of all workflows from n8n.
- **create_workflow**: Creates a new workflow in n8n.
- **get_workflow**: Gets workflow details by its ID.
- **update_workflow**: Updates an existing workflow.
- **delete_workflow**: Deletes a workflow by its ID.
- **activate_workflow**: Activates a workflow by its ID.
- **deactivate_workflow**: Deactivates a workflow by its ID.

#### Execution Management
- **list_executions**: Displays a list of all workflow executions with filtering capabilities.
- **get_execution**: Gets details of a specific execution by its ID.
- **delete_execution**: Deletes an execution record by its ID.

### MCP Resources

The server also provides the following resources for more efficient context access:

#### Static Resources
- **/workflows**: List of all available workflows in the n8n instance
- **/execution-stats**: Summary statistics about workflow executions

#### Dynamic Resource Templates
- **/workflows/{id}**: Detailed information about a specific workflow
- **/executions/{id}**: Detailed information about a specific execution

## Usage Examples

In the `examples` directory, you'll find examples and instructions for setting up and using n8n Workflow Builder with Claude App:

1. **setup_with_claude.md** - Step-by-step instructions for setting up integration with Claude App
2. **workflow_examples.md** - Simple query examples for working with n8n workflows
3. **complex_workflow.md** - Examples of creating and updating complex workflows

## Troubleshooting

- Make sure you are using npm.
- If you encounter problems, try cleaning the build directory and rebuilding the project:
  ```bash
  npm run clean && npm run build
  ```
- Check that your environment variables in `.env` and `cline_mcp_settings.json` are set correctly.
- If you have problems with Claude integration, check the location of the `cline_mcp_settings.json` file.

## License

This project is distributed under the MIT License.
