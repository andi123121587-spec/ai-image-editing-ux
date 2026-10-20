# Design decisions and evidence

## Problem and background

An interior image edit is constrained by more than the selected object. A useful result must preserve spatial structure, camera framing, scale, lighting, materials, and unrelated furniture while changing a clearly defined target. The interaction therefore needs to communicate both sides of the request: **what changes** and **what stays**.

## Evidence source

The current visual source is the Figma design file `OQFyibG49fomUftKGp2JAl`, Page `01 · Screens` (`3:51`). The three complete frames are:

| Version | Frame | Evidence in the frame |
|---|---|---|
| V1 | `25:4` | Original space, reference input, extracted object, selected placement, fusion preview, pending result, and the first action surface. |
| V2 | `282:2288` | Stage-based flow, placement space, generation scope, preserve-structure toggle, preserved furniture, and lighting confirmation. |
| V3 | `278:1025` | AI understanding, reference, change, preserve chips, generation scope, candidate comparison, Apply, Undo, and History. |

These PNGs were exported directly from those Figma frames on 2026-10-20 and visually checked as 1440 × 1024 complete interface frames. They replace the earlier public-package images; the earlier images are not reused here.

## Iteration logic

### V1 · START — make the workflow visible

The first direction lays out the full chain: original space → reference input → extracted object → selected placement → fusion preview → result. This makes the system’s intermediate states legible and gives the user direct object-level actions. The trade-off is that the user may have to manage a multi-step production workflow instead of simply making a controlled edit.

### V2 · EXPOSE — make the generation contract reviewable

The second direction introduces a stage strip and an AI assistant panel. Before generation, the user can see the target, the generation range, whether the original structure is preserved, which other furniture is kept, and whether lighting is matched. This moves error correction earlier. The trade-off is explanation load: a transparent assistant can become another panel the user must read.

### V3 · NARROW — make the decision reversible

The third direction narrows the active task to the room canvas plus a focused AI assistant. It keeps the reference, the requested change, the preserve priorities, and the generation scope visible; then it makes candidate comparison and the Apply / Undo / History path explicit. This is a shorter decision loop, but it still needs validation that users understand the selected range and can recover confidently from a wrong candidate.

## Task flow and state model

1. Select an object or region in the original space.
2. Add a reference or describe the desired change.
3. Confirm the target and generation scope.
4. Set or review the preserve constraints: structure, camera, doors, ceiling, floor, other furniture, and lighting.
5. Generate multiple candidates.
6. Compare candidates, apply one, or recover through Undo and History.

The state model is intentionally visible: selected target → understood contract → pre-generation confirmation → candidate set → applied result / reversible history.

## AI and user responsibilities

The AI should identify the target, interpret the reference, propose a generation scope, surface likely preserve constraints, and generate candidates. The user remains responsible for confirming the target, correcting the scope, choosing what must stay, comparing candidates, and deciding whether to apply or undo. The interface should expose uncertainty instead of treating an AI interpretation as a final decision.

## Current plan and unvalidated areas

The current design direction is to preserve the V3 decision loop while carrying forward V1’s concrete object manipulation and V2’s pre-generation confirmation. The next validation should test range understanding, preserve-constraint comprehension, candidate comparison, and recovery after a wrong result.

Not yet validated: user research, task success, time-on-task, satisfaction, model quality, real API behavior, online generation, accessibility, responsive behavior, and production implementation. These frames are static design evidence only.
