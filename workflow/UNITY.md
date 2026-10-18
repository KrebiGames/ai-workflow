# Unity and Codex integration

Prefer a working local Unity Editor integration (official Unity CLI/Pipeline when supported). Verify the installed command set before using it; do not guess CLI flags. The Editor bridge is a tool, not a separate AI model.

Reference: https://docs.unity.com/en-us/unity-cli/replace-mcp-server-unity-cli

For the current Unity CLI, open the Unity project and run from its root:

```powershell
unity auth login
unity pipeline install
unity setup codex
unity mcp configure codex
```

The Unity plugin supplies Codex skills; Unity Pipeline and MCP expose Editor commands. Verify availability and the selected Editor/project before acting. See [Windows setup](../README.md#windows-tools).

## Project discovery

Before changing code, inspect `ProjectSettings/ProjectVersion.txt`, `Packages/manifest.json`, `Packages/packages-lock.json`, `.gitmodules`, `git submodule status --recursive`, relevant package `package.json` files, `.asmdef` references and Git status. Initialize missing submodules if authorized. Identify the actual owning repository and pinned commit for every edited file; do not accidentally edit cached or generated copies.

Read only the source, assets, SDK signatures and instruction modules needed for the task. Do not dump the entire project, package cache, scene YAML, test log or dependency tree into AI context. Gather a small targeted excerpt, expand only on a concrete question, and keep a concise project map when it measurably reduces repeated discovery.

## Safe Editor operations

- Use Editor APIs / `SerializedObject` / `SerializedProperty` for Unity-native asset edits where possible. Preserve `.meta` GUIDs, scene/prefab references, package ownership, unsaved work and Quantum-generated-source boundaries.
- Track text assets and `.meta` files; ignore `Library/`, `Temp/`, `Obj/`, `Logs/` and generated builds. Consider Git LFS for large binary assets when needed.
- Do not run a batchmode instance against the same Unity project while it is open in another Editor process. Use the live Editor integration or an isolated checkout/worktree for headless tests.
- Never automatically upgrade dependencies, overwrite scenes, rewrite a whole package or modify secrets/permissions as a troubleshooting shortcut.
- Preserve one authoritative authoring source: SO/AssetObject for Unity-native configuration, and schema-validated external formats only when there is a genuine import/export/persistence need.

## Efficient agent loop

1. Inspect the current state and approved scope.
2. Make one focused change.
3. Run the narrowest relevant compiler/test/scenario check.
4. Correct actionable failures within scope; avoid endless speculative retry cycles.
5. Report a compact diff and structured results. Let the human inspect screenshots/video or test the game in person.

Prefer deterministic, local and non-metered checks. Do not call paid cloud services, external LLMs or vision APIs without approval. For slow or failed checks, preserve log files and pass only concise diagnostic excerpts to the agent. Reduce redundant Unity imports, rebuilds, screenshots and unnecessary repeated repository scans.

**Platform checks:** Editor PlayMode does not establish WebGL/mobile correctness. Test relevant browser loading, CORS, memory, IL2CPP/AOT, codecs and input behavior when the change affects those targets.

A typed Editor bridge (`inspect`, `modify`, `validate`, `run scenario`, `observe`) and a generated project manifest may be added after one real workflow proves they are needed. Avoid generalized frameworks and manually duplicated project state.
