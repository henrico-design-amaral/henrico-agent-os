---
name: repo-hygiene-cleaner
description: Use this skill when a project contains external repositories, agent libraries, skills, generated folders, cache, or files that do not belong to the product repo. It cleans scope without touching product code.
version: 1.0.0
status: official
category: repo-hygiene
---

# Repo Hygiene Cleaner

## Purpose

Remove or quarantine files that do not belong to the active project.

## When to use

Use when the repository contains:

- cloned external skill libraries
- agent folders
- prompt collections
- tool caches
- generated archives
- old prototypes
- unrelated projects
- accidental nested repositories

## Process

1. Confirm active project path.
2. Run Git status.
3. Detect nested Git repositories and submodules.
4. List suspicious folders.
5. Classify each item:
   - product file
   - documentation
   - memory
   - external library
   - cache
   - archive
   - unknown
6. Move risky external material to quarantine outside the project.
7. Update `.gitignore`.
8. Update local memory and changelog.
9. Do not change product code.

## Output

Return:

- folders found
- tracked or untracked status
- moved/deleted/quarantined items
- `.gitignore` updates
- memory updates
- commit recommendation
