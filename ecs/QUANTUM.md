# Photon Quantum profile

Read only in a project whose `docs/PROJECT.md` selects **Quantum**. Confirm the installed SDK, preview branch and actual API signatures before editing; Quantum changes across minor/preview versions.

- Quantum simulation is the authoritative deterministic ECS. Components, signals, asset refs and relevant types are defined in `.qtn` and supported simulation C#; inspect generated code rather than editing it directly.
- Use Quantum deterministic math (`FP`, `FPVector*` and relevant Quantum APIs) inside authoritative simulation. Do not use Unity physics, `UnityEngine.Random`, `Time.deltaTime` or platform-dependent state as authoritative gameplay logic.
- Quantum asset classes (`AssetObject`) integrate with Unity SO authoring but are **immutable runtime simulation configuration**, referenced through Quantum asset IDs/refs. Keep mutable state in Quantum components, not the asset.
- Make input authoritative through Quantum's supported input/command mechanisms. Bot and scenario playback must enter through supported simulation paths and deterministic frame/tick scheduling.
- Use Unity-facing components for rendering, camera, audio, visual effects, controls and Editor tooling. Keep their state downstream of simulation state, except for explicitly defined input/configuration boundaries.
- Register simulation systems in the project's actual supported system configuration/runner. Changes must respect predicted/verified frames, rollback and resimulation where applicable.
- Do not substitute Rigidbody/Unity joints for Quantum physics. Distinguish deterministic Quantum collider/physics and KCC processors from visual-only Unity objects.
- Preserve `.qtn` source, `.meta` GUIDs and generated-source boundaries. Keep naming, signals and prototype fields aligned with existing project code.
- Tests should run deterministic fixed-tick simulation cases; assert state and (where practical) that replaying identical inputs yields identical results. Unity PlayMode tests are **not** substitutes for Quantum simulation tests.
- For scenarios: one tick-domain driver, continuous input tracks, bot SDK integration through supported interfaces and deterministic capture/replay. UI/camera tracks remain outside deterministic simulation authority.

**Never** use Friflo `EntityStore`, `QuerySystem` or Unity SO mutation as shortcuts into the Quantum simulation.

References:
- https://doc.photonengine.com/quantum/v3/manual/assets/assets-simulation
- https://doc.photonengine.com/quantum/v3/manual/assets/assets-unity
