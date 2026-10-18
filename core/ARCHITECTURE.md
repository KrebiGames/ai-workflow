# Unity architecture

**Default: ECS runtime + native Unity authoring + automated tests + executable scenarios.** Prefer small composable systems over OOP gameplay hierarchies. Select the project's ECS implementation in `docs/PROJECT.md`.

- **Components:** small, data-oriented runtime state and references, appropriate to the selected ECS.
- **Systems:** behavior with inspectable registration/order. Keep components and systems separate when practical.
- **Authoring:** ScriptableObjects/Quantum AssetObjects for reusable definitions and settings; inline serialized values for one-off configuration; prefabs/scenes/UXML for Unity visuals. An SO is not required for every ECS component.
- **Adapters:** explicit boundaries between simulation/application state and Unity UI, rendering, cameras, input, external services and persistence.
- **Data:** one authoritative source for each field. JSON or other schemas may support import/export or runtime storage, but must not create silently conflicting parallel definitions.
- **Scenarios/tests:** runnable checks for real behavior, not only visual demonstrations.

Keep module organization appropriate to the project; avoid forced folder migrations, unnecessary abstractions and implicit singletons. Keep identifiers and asset GUIDs stable, make system state inspectable, and handle missing references explicitly.

**For each feature establish:** authoring, ECS instantiation/updates, input authority, behavior, verification, rollback and target-platform constraints. Technical choices not shared by all projects belong in `docs/PROJECT.md`.
