## CRITICAL RULES

### Coding Conventions
- Avoid excessive logging. Only log at important decision points or when errors occur.
- Do not use `goto`; follow SOLID principles.
- Files should be opened and saved using UTF-8 encoding

### MCP Servers
- Always use Context7 MCP when library/API documentation, code generation, setup, or configuration steps are needed, without requiring me to ask explicitly.
- You have access to MCP tools called `microsoft_docs_search`, `microsoft_docs_fetch`, and `microsoft_code_sample_search` - these tools allow you to search through and fetch Microsoft's latest official documentation and code samples, and that information might be more detailed or newer than what's in your training data set. When handling questions around how to work with native Microsoft technologies, such as C#, F#, ASP.NET Core, Microsoft.Extensions, NuGet, Entity Framework, the `dotnet` runtime - please use these tools for research purposes when dealing with specific / narrowly defined questions that may occur.

### Agent Customization
- Whenever you exit Plan mode, always save the plan to `./docs/<feature-name>/plan-<feature-name>.md`.
- While implementing, keep the markdown plan file updated with completed progress and any plan changes.
- At the end of every session, if the agent made mistakes or learned a reusable technique, append a short entry to `AGENTS.md` under `## Common Errors & Learnings`.
- Keep each learning entry concise and actionable: include `Date`, `Issue/Learning`, `Root Cause`, and `Prevention Rule`.
- New entries must be appended (do not overwrite older entries) so `AGENTS.md` remains a living document.

## File Index

- `AGENTS.md` - Agent working rules and session-level learnings.
- `README.md` - Project overview and getting-started notes.
- `.agents/README-codex.md` - Codex-specific agent guidance for this repo.
- `.github/README-copilot.md` - Copilot-oriented workflow notes.
- `./docs/<feature-name>/plan-<feature-name>.md` - Current feature plan and progress log (create/update when working in Plan mode).
- `skills/<skill-name>/SKILL.md` - Skill-specific workflow and checklists (if present).

## Common Errors & Learnings

<!-- Append new session learnings below this line using this format:
- Date: YYYY-MM-DD
  Issue/Learning: <what went wrong or what new technique worked>
  Root Cause: <why it happened>
  Prevention Rule: <clear rule for future agents>
-->

## Project Overview

## Development Commands

### Managing Secrets

X API Bearer Token and other secrets should use User Secrets:

```bash
dotnet user-secrets set "<ExampleService>:BearerToken" "YOUR_TOKEN"
```

Never commit secrets to `appsettings.json`.
