# ai-workflow

Shared Unity development rules: **ChatGPT → Codex → Unity tests/scenarios → review**. Architecture: **ECS + ScriptableObject/AssetObject**, with Friflo and Quantum profiles.

## 1. Install tools (Windows, once)

In PowerShell:

```powershell
winget install -e --id Unity.CLI
powershell -ExecutionPolicy Bypass -Command "irm https://chatgpt.com/codex/install.ps1 | iex"
```

Restart PowerShell, then:

```powershell
codex --version
unity --version
codex
```

Sign in to Codex with ChatGPT, then exit.

## 2. Install ai-workflow in each Unity project

From the **Unity project's Git root**:

```powershell
git submodule add -b main https://github.com/KrebiGames/ai-workflow.git .ai/ai-workflow
if (!(Test-Path AGENTS.md)) { Copy-Item .ai/ai-workflow/templates/PROJECT_AGENTS.md AGENTS.md }
if (!(Test-Path docs/PROJECT.md)) { New-Item -ItemType Directory -Force docs | Out-Null; Copy-Item .ai/ai-workflow/templates/PROJECT.md docs/PROJECT.md }
```

Fill in `docs/PROJECT.md` (Friflo or Quantum), then commit the new files and submodule. The shared repository must contain a committed `main` branch and the two templates above.

## 3. Connect Unity and Codex (once per project)

Open the project in Unity Editor. From that same project root:

```powershell
unity auth login
unity pipeline install
unity setup codex
unity mcp configure codex
unity doctor
```

Restart Codex, then run `codex` from the project folder. Optional desktop UI: `codex app`.

**If `CODEX_NOT_FOUND`:** reopen PowerShell and check `codex --version` before running `unity setup codex`. If still missing, reinstall Codex using step 1.

## 4. Clone or update

After cloning a Unity project:

```powershell
git submodule update --init --recursive
```

Update the shared rules:

```powershell
git submodule update --remote .ai/ai-workflow
git add .ai/ai-workflow
git commit -m "Update ai-workflow"
```

## Start a ChatGPT task

```text
Workflow: https://github.com/KrebiGames/ai-workflow
Project: [UNITY_PROJECT_URL or NEW PROJECT]
Request: [IDEA / FEATURE / BUG / EXPERIMENT]
Reference (optional): [ISSUE / PR / ERROR]

Read the relevant workflow and project code first. Agree on design, implementation and verification before changing code.
```

Small approved fixes stay in Codex. Use GitHub Issues for substantial tasks; no permanent task files.
