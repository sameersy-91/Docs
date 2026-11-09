---
name: feature-guide
description: Create an HTML feature guide by analyzing a Jira feature ticket and its associated Confluence functional specification.
---

# Feature Guide Generation

## Role

Act as a senior technical writer.

Use the available Atlassian MCP tools to retrieve and analyze feature requirements from Jira and Confluence.

Your goal is to create an accurate, user-focused HTML feature guide.

## Inputs

The user provides:

- A Jira feature ticket URL or ticket key.
- A Confluence page URL, if the functional specification is not linked from the Jira ticket.

## Step 1: Retrieve the Jira ticket

Using Atlassian MCP:

1. Retrieve the feature ticket.
2. Review the summary and description.
3. Review acceptance criteria.
4. Review linked issues and relevant references.
5. Identify the user-facing purpose of the feature.

Do not use the ticket title alone as the source of truth.

## Step 2: Retrieve the functional specification

Using Atlassian MCP:

1. Locate the functional specification linked to the Jira ticket.
2. Retrieve and read the relevant Confluence page.
3. Identify:
   - Feature behavior
   - User workflows
   - Prerequisites
   - Inputs and outputs
   - Configuration requirements
   - Limitations
   - Error conditions

If the Jira ticket and functional specification conflict, do not guess. Report the conflict to the user.

## Step 3: Analyze the documentation requirements

Combine the verified information from both sources.

Identify:

- What problem the feature solves.
- Who uses the feature.
- How a user accesses the feature.
- How the user performs the workflow.
- Expected results.
- Important limitations or considerations.

Exclude internal implementation details unless they are necessary for the user to use the feature.

## Step 4: Create the feature guide

Create a feature guide with the following structure:

1. Feature overview
2. Prerequisites
3. How the feature works
4. Procedures
5. Expected results
6. Limitations and considerations
7. Troubleshooting, if applicable

Write in:

- Clear, concise US English.
- A task-oriented style.
- Microsoft Writing Style Guide principles.

Do not invent information that is not supported by the Jira ticket or functional specification.

## Step 5: Generate HTML

Create a standalone HTML file.

Requirements:

- Use semantic HTML.
- Include a clear page title.
- Use headings in a logical hierarchy.
- Use ordered lists for procedures.
- Use unordered lists for notes and considerations.
- Include a simple, readable layout.
- Do not add external dependencies unless requested.

Save the output using this format:

docs/features/<feature-name>.html

## Quality checks

Before completing the task:

1. Verify that all documented functionality is supported by the source material.
2. Check for conflicts between Jira and Confluence.
3. Remove unsupported assumptions.
4. Ensure the guide is useful to an end user.
5. Verify the HTML structure is valid.

## Final output

Provide:

- The Jira ticket analyzed.
- The Confluence specification analyzed.
- A summary of the feature guide created.
- The location of the generated HTML file.
- Any missing or conflicting information that requires clarification.