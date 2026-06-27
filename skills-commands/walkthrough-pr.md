---
name: walkthrough-pr
description: Reads Pull Requests (PRs) changes, gather codebase context, split changes into smaller chunks, explain them one-by-one awaiting user confirmation for each.
metadata:
  version: "1.0"
---

# Walkthrough PR Skill

## When to use

- Use this skill when the user prompts you to review or walkthrough a Pull Request.
- This skill is helpful to make sure the user understands the changes inside a Pull Request.

## Instructions

1. Inputs:
  a. expect the user to bring a repository and a specific branch other than main/master. If given a pull request link, try to pull the repository and branch from it. Don't continue without these two pieces of information.
  b. optionally, the user may indicate you to be verbose (explicitly or using `-v` or `--verbose`).

2. Setup:
  a. make sure your directory contains the required repository, otherwise clone it. If you don't have the required URL to clone it, ask the user to provide it.
  b. checkout the main branch (master otherwise), run `git remote update && git pull` to make sure it's up to date.
  c. checkout the specific branch with the changes of the PR, make sure it is also up to date.

3. Gather knowledge:
  a. run `git diff origin/main` to get the PRs changes.
  b. gather contextual knowledge from the repository's codebase.

4. Prepare walkthrough:
  a. split the PR changes in small and progressive chunks following the format:
    - title: short title, example "Part 1".
    - context (verbose only): explain the context regarding the relevant code/changes (<100 words).
    - introduction: give a brief description of the changes (<20 words).
    - code snippets: reference files and lines of code, using snippets that must not sum up more than 100 lines of code.
    - full explanation: give a full and detailed explanation of what has changed, its impact, and relevance to the PR (<100 words).
  b. omit non-source code changes like documentation, versioning, etc.

5. Walk the user through the prepared chunks:
  a. present one chunk at a time to the user and prompt they to ask questions or indicate they're ready to continue.
  b. if the user asks for clarifications, respond them and ask again if they have further questions or should continue with the next chunk.

6. Wrap-up:
  a. once the user confirmes the last piece of changes is okay, proceed to wrap-up.
  b. prepare a final conclusion regarding the PR changes and wether or not they should be approved or not, including potential comments or questions.
  c. checkout the main branch of the repository.
  d. present the conclusion to the user.
