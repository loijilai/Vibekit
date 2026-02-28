## 🚨 CRITICAL RULES

- Avoid excessive logging. Only log at important decision points or when errors occur.
- Do not use `goto`; follow SOLID principles.
- Always use Context7 MCP when library/API documentation, code generation, setup, or configuration steps are needed, without requiring me to ask explicitly.
- Whenever you exit Plan mode, always save the plan to `./docs/<feature-name>/plan-<feature-name>.md`.
- While implementing, keep the markdown plan file updated with completed progress and any plan changes.

## Project Overview

## Development Commands

### Managing Secrets

X API Bearer Token and other secrets should use User Secrets:

```bash
dotnet user-secrets set "<ExampleService>:BearerToken" "YOUR_TOKEN"
```

Never commit secrets to `appsettings.json`.
