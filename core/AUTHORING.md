# Authoring for designers, developers and agents

The Unity Editor is the default source of truth for Unity-native assets. Agents should be able to discover, create and validate the **same assets** designers edit, rather than maintain parallel AI-only data structures.

| Need | Preferred representation |
| --- | --- |
| Reusable definitions, profiles, scenarios | ScriptableObject / Quantum AssetObject |
| Small configuration used in one place | Inline serializable data |
| Polymorphic inline data | `[SerializeReference]` when justified and validated |
| Visual content | Scenes, prefabs, UXML, materials and other native assets |
| Imported, generated or runtime-persisted data | Validated, versioned JSON or a documented source format |
| Complex authoring UX | Custom Inspector/graph/timeline over an existing authoritative definition |

**ECS boundary:** authoring definitions initialize/configure ECS data; they do not replace ECS component state. Friflo may map SO definitions into its `EntityStore`. Quantum uses native deterministic `AssetObject`/`.qtn` paths; simulation assets must not become mutable runtime state.

**Agent asset edits:** inspect the real asset/schema and preserve GUIDs; prefer Editor APIs and typed actions over blind `.asset`/`.unity` YAML edits. Check ranges, missing or circular references, incompatible components and stable identifiers. Present meaningful before/after changes and support Undo/Git rollback.

**Play mode:** changing runtime ECS state and editing a saved SO are distinct operations. Provide Apply / Revert / Save as new definition when interactive tuning is needed. In Quantum, configuration changes must respect deterministic frame/asset rules and may require a restart/replay.

**Builds/WebGL:** packaged players cannot write back into authoring `.asset` files. Use an explicit, versioned runtime store or backend for user changes. Never promise persistence without an implemented save path.
