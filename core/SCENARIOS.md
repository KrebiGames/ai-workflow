# Executable scenarios

Scenarios represent repeatable behavior over time: setup/reset, actors, steps or parallel input tracks, duration/timeout, expectations, optional captures and cleanup. Use native Unity authoring assets where suitable; share concepts between ECS profiles, not incompatible runtime APIs.

- Drive actors through their real input/command path. Keep fixture setup separate from behavior under test.
- **Quantum:** inputs advance in fixed simulation ticks; use deterministic capture/replay and comparable checksums when supported by the installed version. UI, camera and Unity Timeline remain outside simulation authority.
- **Friflo:** execute actual registered ECS systems over explicit step/time inputs, with isolated state for each run.
- Prefer state-based assertions and tolerances over fragile exact transform values for physics/KCC cases. Every scenario returns concise structured results (`passed`, `failed`, `not_run`, `unsupported`).
- Record screenshots/video only as optional artifacts for humans, never as required AI inputs.
- Expand to bots, nesting, parallel tracks or Timeline only when a concrete scenario demands it. A scenario runner is not a replacement for the Quantum Bot SDK visual editor.

Start with one end-to-end scenario and add capabilities incrementally. Tests must declare prerequisites instead of relying on state left by a previous scenario.
