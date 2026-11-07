---
name: update-user-guide
description: Analyze code changes in a pull request and update the product user guide based on verified user-facing changes.
---

# Update User Guide from a Pull Request

## Objective

Analyze the specified pull request and determine whether the code changes affect the product user experience or documented functionality.

## Instructions

1. Review the pull request diff and the relevant source code.
2. Identify user-facing functionality that was added, changed, or removed.
3. Compare the changes with the existing user guide.
4. Update only the sections affected by verified code changes.
5. Do not document internal implementation details.
6. Do not invent functionality that is not supported by the code.
7. Preserve the existing structure and writing style of the user guide.
8. Follow Microsoft Writing Style Guide principles and use US English.

## Verification

Before completing the update:

- Verify that each documentation change is supported by the source code.
- Identify any assumptions or functionality that cannot be confirmed.
- Do not modify unrelated sections.

## Output

Update:

docs/user-guide.md

After updating the file, provide a summary containing:

- The user-facing changes identified in the PR.
- The documentation sections updated.
- Any changes that do not require documentation.