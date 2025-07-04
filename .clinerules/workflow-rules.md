## Brief overview
This document provides guidelines for creating standardized Cline workflow files. Workflows are stored in the `.clinerules/workflows` directory and follow a specific structure to ensure consistency and proper execution.

## Workflow file structure
- All workflow files must be placed in the `.clinerules/workflows` directory
- Files should be named descriptively with kebab-case (e.g., `generate-trace-report-by-workitem.md`)
- It is recommended to create workflows for common, multi-step tasks to promote automation and consistency.
- Each workflow must be enclosed in `<task>` tags with a `name` attribute
- The task objective must be enclosed in `<task_objective>` tags
- The detailed sequence steps must be enclosed in `<detailed_sequence_steps>` tags
- The entire workflow should follow proper markdown formatting conventions

## Task definition
- Begin each workflow file with `<task name="Descriptive Task Name">`
- End each workflow file with `</task>`
- The task name should be concise but descriptive of the workflow's purpose
- Example: `<task name="Generate Trace Report by Workitem">`

## Task objective
- The task objective section should be enclosed in `<task_objective>` tags
- Provide a clear, concise description of what the workflow aims to accomplish
- Include any key tools or resources that will be used (e.g., MCP tools)
- Specify the expected output format (e.g., markdown file)
- Keep the objective to 1-3 sentences for clarity

## Detailed sequence steps
- The detailed steps section should be enclosed in `<detailed_sequence_steps>` tags
- Begin with a level 1 heading that includes the workflow name and "Process - Detailed Sequence of Steps"
- Organize major steps as level 2 headings (##) with sequential numbering
- Use numbered lists for substeps under each major step
- Indent sublists by 4 spaces
- Surround all headings with newlines for proper formatting
- Surround all code blocks with newlines

## Tool usage conventions
- Explicitly reference tools using backticks (e.g., `ask_followup_question`)
- For user interaction, use the `ask_followup_question` tool
- For accessing external data, use appropriate MCP tools (e.g., `use_mcp_tool`)
- For file operations, specify directory checks and file creation steps
- Always end workflows with the `attempt_completion` tool to present results

## Step formatting
- Major steps should follow a logical sequence
- Each major step should have a clear purpose
- Substeps should provide specific actions to take
- Include examples where helpful (e.g., example IDs, formats)
- For output generation steps, clearly specify:
  - Directory structure and creation
  - File naming conventions
  - Content structure with detailed subsections

## Example workflow structure
```markdown
<task name="Example Workflow">

<task_objective>
Brief description of what this workflow accomplishes and its output.
</task_objective>

<detailed_sequence_steps>
# Example Workflow Process - Detailed Sequence of Steps

## 1. First Major Step

1. First substep with specific action.
   
2. Second substep with specific action.

## 2. Second Major Step

1. First substep with specific action.
   
2. Second substep with specific action.
   - Additional detail or example

## 3. Generate Output

1. Organize outputs under the root directory outputs/ 

2. Check if output directory exists, create if needed.

3. Create output file with specified content:
   i. First content section
   ii. Second content section
   iii. Third content section

4. Use the `attempt_completion` command to present results.

</detailed_sequence_steps>

</task>

## Available Tools

**General Cline Tools:**

- **execute_command**: Execute CLI commands on the system
- **read_file**: Read the contents of a file
- **write_to_file**: Create new files or overwrite existing ones
- **replace_in_file**: Make targeted edits to specific parts of a file
- **search_files**: Perform regex searches across files in a directory
- **list_files**: List files and directories within a specified directory
- **list_code_definition_names**: List definition names in source code files
- **browser_action**: Interact with a Puppeteer-controlled browser
- **ask_followup_question**: Ask the user for additional information
- **attempt_completion**: Present the result of completed work
- **new_task**: Create a new task with preloaded context
- **plan_mode_respond**: Respond to user inquiries in PLAN MODE
- **load_mcp_documentation**: Load documentation about creating MCP servers
