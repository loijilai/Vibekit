## CRITICAL RULES

### Coding Conventions

- Avoid excessive logging. Only log at important decision points or when errors occur.
- Do not use `goto`; follow SOLID principles.
- Files should be opened and saved using UTF-8 encoding
- **If statements must always use braces**: Use `if (condition) { statement; }` instead of `if (condition) statement;` — braces are mandatory for all if statements to improve readability and prevent subtle bugs
- **Controllers must stay thin**: Controllers are only responsible for receiving requests, validating boundary input, and passing work to services. Do not place business logic in controllers, and avoid controller-internal concerns such as detailed logging, `Stopwatch` timing, or workflow orchestration unless there is a clear framework-level requirement. Move business logic to the service layer to keep controllers lightweight and make behavior easier to test.
- **Projects must follow layered folders**: Application code must be organized into `Controllers`、`Services`、`Repositories`、`Clients` and other clearly named folders by responsibility. Do not place controller, service, repository, or client implementation classes inside `Program.cs`.
- **Program.cs must stay as composition root only**: `Program.cs` is only responsible for service registration, middleware / pipeline setup, configuration wiring, and app startup. Do not place request handling logic, business logic, data access logic, or external API calling logic in `Program.cs`.
- **Configuration must use Options Pattern**: Always use `AddOptions<T>()` with `.Bind()`, `.ValidateDataAnnotations()`, and `.ValidateOnStart()` for configuration binding. Example:
  ```csharp
  builder.Services.AddOptions<KeyOptions>()
      .Bind(builder.Configuration.GetSection(KeyOptions.Key))
      .ValidateDataAnnotations()
      .ValidateOnStart();
  ```
  This ensures type-safe configuration, validation at startup, and prevents runtime configuration errors

### MCP Servers

- Always use Context7 MCP when library/API documentation, code generation, setup, or configuration steps are needed, without requiring me to ask explicitly.
- You have access to MCP tools called `microsoft_docs_search`, `microsoft_docs_fetch`, and `microsoft_code_sample_search` - these tools allow you to search through and fetch Microsoft's latest official documentation and code samples, and that information might be more detailed or newer than what's in your training data set. When handling questions around how to work with native Microsoft technologies, such as C#, F#, ASP.NET Core, Microsoft.Extensions, NuGet, Entity Framework, the `dotnet` runtime - please use these tools for research purposes when dealing with specific / narrowly defined questions that may occur.

### Communication Style

- Always provide both code and explanation together. Never give code without explaining the design decisions behind it.
- The user is a junior developer — explain _why_ a pattern or approach is chosen, not just _what_ the code does.
- When multiple approaches exist, briefly compare them and justify the recommended choice.
- Always explain the root cause of problems and aim to teach the user, so the user can understand and grow.

### Git Commit 規範

所有 Commit Message 必須使用繁體中文，並使用台灣常用文字（例如「程式碼」而非「代碼」）。

#### 第一行（Header）

- 全程使用繁體中文，必須包含**類型（type）**與**主旨（subject）**，且不超過 50 個字。
- 格式：`<type>：<subject>`
- 寫完後空一行再接 Body。

#### 類型（type）定義

| 類型       | 說明                                                                                            |
| ---------- | ----------------------------------------------------------------------------------------------- |
| `feat`     | 新功能、修改功能。增加新的程式碼，用於開發新的功能、支援方法或介面。                            |
| `refactor` | 重構、優化。對程式碼進行結構性優化、提升可讀性或維護性，但不改變功能行為。                      |
| `fix`      | 修復 Bug。修正程式中的錯誤或異常行為。                                                          |
| `docs`     | 註解、文件、版號。專門為文件、註解或版本號更新的 Commit。一般開發過程中附帶修改可不必特別指出。 |
| `style`    | Coding 格式調整、風格調整。調整程式碼排版、搬移參數等，不影響程式運作。                         |
| `test`     | 測試。新增或修改測試，例如單元測試、整合測試。                                                  |
| `chore`    | 套件、專案版本升級。專案版本或套件的升級，連帶改動也算入此類。                                  |
| `revert`   | 恢復上一版。當需回溯一個或多個版本時使用。                                                      |
| `merge`    | 合併 Code。用於程式碼的合併操作。                                                               |
| `sync`     | 主、支合併 Bug。解決分支間衝突時使用。                                                          |

#### Body（第三行起）

- 使用繁體中文，使用數字條列。
- 每一列先說明**為什麼修改**，再說明**修改了什麼**，講重點。
- 每項不超過 50 字，不超過三項。

#### 撰寫參考範例

```
fix：修正取用基準日規則，將當天調整為美國五天前的交易日

1. 原程式會抓取週期當天為基準日去做下市條件判斷，
   但需判斷五天內收盤是否有行情，故將基準日改為美國五天前的交易日
```

### Agent Customization

- Whenever you exit Plan mode, always save the plan to `./docs/<feature-name>/plan-<feature-name>.md`.
- While implementing, keep the markdown plan file updated with completed progress and any plan changes.

## File Index

- `AGENTS.md` - Agent working rules and session-level learnings.
- `README.md` - Project overview and getting-started notes.
- `./docs/<feature-name>/plan-<feature-name>.md` - Current feature plan and progress log (create/update when working in Plan mode).

## Project Overview

### Project Structure Principles

- `Dtos`：放 API request / response。DTO 是對外契約，負責邊界資料交換，不承擔 domain model 責任。
- `Controllers`：只處理 HTTP request / response、模型繫結、邊界驗證與呼叫 service，不可放商業邏輯。
- `Services`：放真正執行流程的服務類別，集中業務流程協調與主要應用邏輯。
- `Services/Models`：放只給 service 內部使用的資料模型，避免內部流程資料外漏成公開契約。
- `Repositories`：放資料存取邏輯，負責與資料庫、快取或持久化媒介互動，不可承擔 controller 或 service 的責任。
- `Clients`：放對外部 API、第三方系統或 SDK 的呼叫封裝，避免外部整合細節散落在 service 或 `Program.cs`。
- `Options`：放設定綁定型別，集中管理組態對應結構，避免散落在各 service 內。
- `Exceptions`：放自訂例外，避免例外型別混進 service 檔案，讓錯誤語意更清楚。
- `Utilities`：放純工具類別，例如 resolver 這類輔助邏輯，不承載主要流程責任。
- `Program.cs`：只保留 DI 註冊、middleware、組態與啟動流程，不可直接寫 controller、service、repository、client 的實作。
- 原則總結：入口在 `Controllers`，商業流程在 `Services`，資料存取在 `Repositories`，外部整合在 `Clients`，`Program.cs` 只負責組裝。

## Development Commands

### Managing Secrets

X API Bearer Token and other secrets should use User Secrets:

```bash
dotnet user-secrets set "<ExampleService>:BearerToken" "YOUR_TOKEN"
```

Never commit secrets to `appsettings.json`.

### Time Format

Use DTOs to handle external time formats such as Unix seconds, Unix milliseconds, or API-specific timestamp strings. Convert them at the boundary, and keep a single internal domain representation for all business logic and time calculations.
