# VibeKit

AI-assisted coding tools and workflows.

## Sample Workflow

`*` means optional.

### Setup

1. Clone this repo, then copy `.agents` and `.github` into your project folder.
2. Browse skills at https://skills.sh/
3. MCP Server
   - Install the Context7 MCP server
   - Install [Microsoft Learn MCP server](https://github.com/MicrosoftDocs/mcp?tab=readme-ov-file)

### Development

4. `*` Design with Pencil: install the Pencil extension from the VS Code Extensions marketplace.
5. Start with Plan mode. See [AGENTS.md](AGENTS.md) for tips on automatically generating `plan.md`.
6. Review the plan: run `/clear`, then ask the agent to critique the plan against requirements and detect overengineering (a common issue). Repeat this twice, focus on repeated feedback, and use it to refine the markdown.
7. Implement and commit changes to source control.
8. Run code review with `/review`

## References

### Useful Prompts

#### Phase 1. Research

```
Understand the code base by reading the repository in depth, understand how it works deeply, what it does and all its specificities. when that’s done, write a detailed report of your learnings and findings in `./docs/research.md`
```

```
study the notification system in great details, understand the intricacies of it and write a detailed research.md document with everything there is to know about how notifications work
```

#### Phase 2. Planning

```
I want to build a new feature <name and description> that extends the system to perform <business outcome>. write a detailed plan.md document outlining how to implement this. include code snippets
```

Annotation Cycle:

```
I added a few notes to the document, address all the notes and update the document accordingly. don’t implement yet
```

Todo List:

```
add a detailed todo list to the plan, with all the phases and individual tasks necessary to complete the plan - don’t implement yet
```

#### Phase 3. Implement

```
implement it all. when you’re done with a task or phase, mark it as completed in the plan document. do not stop until all tasks and phases are completed.
```

- https://boristane.com/blog/how-i-use-claude-code/
