# VibeKit

AI-assisted coding tools and workflows.

## Sample Workflow

`*` means optional.

### Setup

1. Clone this repo, then copy `.agents` and `.github` into your project folder.
2. Browse skills at https://context7.com/skills.

   Example:
   - https://context7.com/skills/wshobson/agents/dotnet-backend-patterns

3. Install the Context7 MCP server from the VS Code Extensions marketplace.

### Development

4. `*` Design with Pencil: install the Pencil extension from the VS Code Extensions marketplace.
5. Start with Plan mode. See [AGENTS.md](AGENTS.md) for tips on automatically generating `plan.md`.
6. Review the plan: run `/clear`, then ask the agent to critique the plan against requirements and detect overengineering (a common issue). Repeat this twice, focus on repeated feedback, and use it to refine the markdown.
7. Implement and commit changes to source control.
8. Run code review with `/review`
