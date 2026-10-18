# Friflo ECS profile

Read only in a project whose `docs/PROJECT.md` selects **Friflo ECS**.

- The ECS runtime is `Friflo.Engine.ECS`; follow the **actual pinned package version**, not remembered APIs from another version.
- Entities and state live in an `EntityStore`, with data components implementing the package's appropriate component interface/pattern. Group/update systems using `SystemRoot`/`SystemGroup` if adopted by the project. Do not replace a working project-specific system set just to follow documentation examples.
- Keep component data and behavior separate; minimal Unity-dependent code in systems. Unity transforms, UI Toolkit elements and scene objects are accessed through adapters/bridges with explicit ownership and lifecycle.
- SO entity definitions and component configurations are **authoring** input; instantiate/update the `EntityStore` through a small, testable mapping layer. Do not assume Friflo components are themselves SOs.
- Preserve stable entity identifiers used by persisted JSON, UI routing or external integrations. Clarify when using ephemeral runtime Entity IDs versus exported IDs.
- Structural changes during iteration should follow the selected Friflo API's safe patterns (such as command buffers) and the actual installed version.
- Systems lists/order are configured in one inspectable source (SO/editor configuration if the project supports it), with a clear runner bootstrap. Avoid hidden registration through multiple unrelated scripts.
- In tests, create fresh `EntityStore` instances and update the actual systems; assert on ECS state and separately test Unity-facing adapters.
- When generating or parsing JSON, treat schemas, migrations, unknown components and compatibility explicitly. If a system cannot interpret a component, report that clearly.

**Never** import Quantum-specific tick, `Frame`, `FP`, `AssetRef`, QTN or deterministic networking rules into a Friflo project unless separately requested.

Reference: https://github.com/friflo/Friflo.Engine.ECS
