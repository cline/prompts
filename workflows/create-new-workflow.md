<task name="Create New Workflow">

<task_objective>
Guide the user through the process of creating a new standardized Cline workflow file according to the established conventions. The output will be a properly structured workflow file in the .clinerules/workflows directory.
</task_objective>

<detailed_sequence_steps>
# Create New Workflow Process - Detailed Sequence of Steps

## 1. Define Workflow Purpose

1. Use the `ask_followup_question` command to ask the USER for the purpose of the new workflow.
   
2. Use the `ask_followup_question` command to ask the USER for a concise name for the workflow.
   
3. Determine the appropriate filename using kebab-case format (e.g., `analyze-system-requirements.md`).

4. Inform the USER of the upcoming workflow file creation process and the main steps they will be asked to complete.

## 2. Define Task Objective

1. Use the `ask_followup_question` command to ask the USER for the primary objective of the workflow. Remind the user to provide breadcrubs of the inputs to be used, the output to be generated, and a generalization of the processing to formulate the outputs.
   
2. Use the `ask_followup_question` command to ask the USER if know what MCP servers will be required at this point by providing of a list of Cline's active MCP server names.
   
3. Use the `ask_followup_question` command to ask the USER what the expected output format will be (e.g., markdown file, code file, terminal output).
   
4. Formulate a clear, concise task objective statement (1-3 sentences) based on the USER's responses.

## 3. Outline Major Steps

1. Use the `ask_followup_question` command to ask the USER to list the major steps in the workflow (3-7 steps recommended) and they will have a oppurtunity provide more details later or let Cline determine this for them
   
2. For each major step, determine the following:
   - Required tools or resources
   - Expected outputs or transitions to the next step

## 4. Define Detailed Substeps

1. For each major step identified and analyzied, present the user what how you intended to perform the step and use the `ask_followup_question` command to see confirmation or clarification.

## 5. Generate Workflow File

1. Determine if the `.clinerules/workflows` directory exists. If not, create it.

2. Create a markdown file named `.clinerules/workflows/{{workflow-filename}}.md` with the following structure:
   i. Task definition with name attribute
   ii. Task objective section
   iii. Detailed sequence steps section with proper formatting
   iv. Proper tool references and formatting conventions

3. Use the `read_file` command to read the `.clinerules/workflow-template.md` file to ensure the new workflow follows all conventions.

4. Use the `write_to_file` command to write the completed workflow file.

5. Use the `attempt_completion` command to present the USER with the completed workflow file and confirmation of its creation.

</detailed_sequence_steps>

</task>
