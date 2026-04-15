---
name: prototype-implement
description: Implement code from a Builder URL. Use when the user asks to implement, build, or generate code from a Builder project URL, even if they do not explicitly mention this skill.
---

# Prototype Implement

## Quick Start
1. Ask the user for a prototype URL.
2. Validate it matches this format:
   - `https://builder.io/app/projects/{projectid}/{path}`
   - Regex: `^https:\/\/builder\.io\/app\/projects\/[^\/]+\/.+$`
3. If invalid, tell the user to provide a URL copied from Builder in that exact format.
4. If valid, ask what they want to do with the prototype.
5. Use their response as `{prompt}` and run:

```bash
npx "@builder.io/dev-tools@latest" code --prototype "{url}" --prompt "{prompt}"
```

## Instructions

### 1) Ask for URL
Prompt the user for a Builder URL.

### 2) Validate URL
A valid URL must match:
- `^https:\/\/builder\.io\/app\/projects\/[^\/]+\/.+$`

Optional extraction helpers:
- projectId: `^https:\/\/builder\.io\/app\/projects\/([^\/]+)\/`
- path: `^https:\/\/builder\.io\/app\/projects\/[^\/]+\/(.+)$`

### 3) Handle invalid URL
If URL does not match, respond with:
- Ask them to provide a URL copied from Builder
- Re-state the required format: `https://builder.io/app/projects/{projectid}/{path}`
- Do not proceed until a valid URL is provided

### 4) Ask for implementation intent
When URL is valid, ask: what do they want to do with the prototype?
Use their full answer as `{prompt}`.

### 5) Run the command
Run exactly:

```bash
npx "@builder.io/dev-tools@latest" code --prototype "{url}" --prompt "{prompt}" --accept
```

Substitute:
- `{url}` with the validated Builder URL
- `{prompt}` with the user’s requested implementation details

## Gotchas
- Do not continue with generation when URL is invalid.
- Preserve user intent in `{prompt}`; do not over-summarize.
- Keep quotes around `{url}` and `{prompt}` to avoid shell parsing issues.
- Ensure the URL uses `https://builder.io/app/projects/` (not other domains/paths).

## Example Flow
1. User: "Implement this prototype"
2. Assistant: "Please share a Builder URL in the format `https://builder.io/app/projects/{projectid}/{path}`"
3. User shares valid URL
4. Assistant: "What would you like me to do with this prototype?"
5. User: "Create native SwiftUI screens"
6. Assistant runs:

```bash
npx "@builder.io/dev-tools@latest" code --prototype "https://builder.io/app/projects/abc123/some/path" --prompt "Create native SwiftUI screens"
```
