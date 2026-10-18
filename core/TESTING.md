# Verification and review

Prefer **machine-readable evidence over model interpretation**. Check only what the change can affect, using the least expensive reliable test first:

1. Source/schema checks, pure logic tests and format/serialization validation.
2. Unity compilation and relevant EditMode tests.
3. Focused PlayMode/ECS tests and executable scenarios.
4. Relevant target-platform smoke tests (WebGL/browser, Windows, Android, etc.).
5. Human visual/game-feel review, where applicable.

A passing source-level check does not prove Unity compilation; a passing Editor test does not prove WebGL or mobile behavior. Do not run expensive full suites or builds after every small change; use them at suitable milestones or before a release.

## Evidence and media

- **Structured assertions, ECS state, error summaries and exit codes are authoritative** for automated verification.
- Save screenshots and video as artifacts **for human review by default**. Do not automatically send them to a vision model, generate visual descriptions, or attach them to every AI handoff.
- Use AI image/video interpretation only on explicit request or when authorized to investigate a specific visual failure that machine checks cannot establish. Prefer one relevant crop/frame over a recording or image batch.
- Capture media only when it helps inspect behavior or compare results; use paths/links and concise metadata in agent reports. Never claim a screenshot proves correctness without appropriate assertions.
- On failures, return the first actionable errors, relevant stack traces and links to complete logs rather than dumping entire Editor logs into model context.

## Delivery evidence

Every implementation handoff should briefly state what changed, checks that **passed / failed / were not run**, where logs/media can be found, and how to revert. Provide an accessible diff/branch/PR for remote review; local-only changes are not visible to another agent.

For Quantum, compare repeat runs/checksums when the installed SDK supports them, and assert robust state invariants for physics (with documented tolerances where needed) rather than brittle pixel-perfect or unnecessarily exact position checks. Friflo can use isolated `EntityStore`/system tests.

Once the local verification loop works, consider CI on pull requests for a focused suite; avoid building a costly CI pipeline before it has a demonstrated benefit. Keep relevant regression scenarios and tests under version control. Store only accepted, durable project decisions in project documentation. GitHub Issues can retain a brief implementation summary.
