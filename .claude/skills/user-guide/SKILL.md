---
name: user-guide
description: Generate a task-based product user guide by analyzing the source code in this repository.
---

# User Guide Generation Skill

## Your role

Act as a senior technical writer. Analyze the application source code and generate a user guide for the product.

Do not assume functionality that is not supported by the source code.

## Audience

Write for end users who want to use the product but may not understand the underlying implementation.

## Instructions

When generating the user guide:

1. Analyze the source code to understand the product's purpose and available functionality.
2. Identify user-facing features and workflows.
3. Do not describe internal code, functions, classes, or implementation details unless they are necessary for users.
4. Write task-based instructions using clear action-oriented headings.
5. Use simple, concise language and US English.
6. Follow the Microsoft Writing Style Guide principles.

## Required structure

Create the user guide with the following sections:

# Product overview

Briefly explain what the product does and who should use it.

# Before you begin

List any prerequisites or information users need.

# Get started

Explain how users can access or start using the product.

# Create a task

Provide steps for creating a task.

# View tasks

Explain how users can view existing tasks.

# Complete a task

Explain how users can mark a task as complete.

# Delete a task

Explain how users can delete a task.

# Troubleshooting

Document common errors that are explicitly identified in the source code.

## Quality checks

Before completing the user guide:

- Verify that every documented feature is supported by the source code.
- Clearly distinguish between confirmed functionality and assumptions.
- Remove unsupported claims.
- Use consistent terminology.
- Ensure the instructions are useful to an end user.

## Output

Create the completed user guide as:

`docs/user-guide.md`