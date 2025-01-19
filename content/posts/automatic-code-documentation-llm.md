---
title: "Automatic code documentation using LLM"
date: 2025-01-19
draft: true

tags: ['personal project', 'llm']
categories: ['Personal Project']
toc: true
---
> Everything is work-in-progress. I'm documenting my thoughts and implementation as I go.

# The idea
I first heard of this idea from Andriy Burkov - https://x.com/burkov/status/1877117229206221076

Instead of spending manual efforts documenting your code, let LLMs look at your git diff to generate and add documentation for you.

These are the outlined steps by Andriy - 
1. New staged changes (`git add`) trigger an LLM call that identifies which Markdown files in the documentation directory are affected by the staged diff (`git diff --cached`).
2. Another LLM call receives both the documentation content and the staged diff, generating updated Markdown content.
3. The developer reviews both the code changes and documentation updates in the staging area, then creates a commit (`git commit`) to approve them together.

My aim is to implement this functionality as a weekend project in order to get my hands dirty with LLMs.

# System architecture

The solution will be implemented as a Git pre-commit hook that processes documentation updates automatically.

## Core Components
- Pre-add hook script
- LLM integration service
    - Diff analysis module (Identifying updates)
    - Documentation update handler (Updating docs)

### Pre-add hook implementation

1. Create the Script

```bash
#!/bin/bash
# .git/hooks/pre-add
python3 run_doc_update.py
```

2. Make Script Executable
```bash
chmod +x .git/hooks/pre-add
```

3. Create Git Alias
```bash
git alias.udpate-and-add '!.git/hooks/pre-add; git add "$@"'
```

#### Usage
Instead of using git add, you'll use:
```bash
git udpate-and-add <files>
```

**Note**: This would allow us to selectively use this doc auto-update functionality. Use `git update-and-add` when you want automatic updates. Use `git add` when you want to change the auto documentation yourself and otherwise.

### LLM Service (TBD)

There are two places where an LLM will be used. 

Firstly, to identify the documents across the repository which need updation. This will be determined by comparing the staged git diff WITH all the markdown files in the repo.

And then, once we find the target documentation, to update the documentation within after corroborating with the staged diff.

#### Diff analysis module
#### Documentation udpate handler

# Challenges
1. The staged diff corresponds to multiple changes. This would require doc updates in multiple files. How can the LLM identify which part of the diff corresponds with which particular documentation?

# Limitations
1. Currently, the LLM will only look at the markdown files in the same directory as the staged diff. So the identification part will be implemented later. Either that or keep only one markdown file as the documentation across the repo.