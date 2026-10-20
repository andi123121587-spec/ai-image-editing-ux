# Design decisions

## Context

This case explores an indoor AI image-editing workflow. A local edit is not only a request to change one object. It also needs a clear boundary around what must remain stable: spatial structure, scale, lighting, materials, and unrelated objects.

The interaction model treats the task as a contract between **change** and **keep**.

## V1 → V2 → V3

| Version | Problem | Change | Trade-off | Validation boundary |
|---|---|---|---|---|
| V1 · START | The generation process and intermediate states were difficult to see. | Expose the chain from source image to reference, extracted object, fusion preview, and result. | More process visibility can turn an interior edit into workflow management. | Design inference; no user walkthrough result is included. |
| V2 · EXPOSE | Users could not easily tell how the system interpreted the reference and the room. | Show AI understanding, reference fit, generation scope, and priority-preserve items before generation. | Earlier correction is possible, but too much explanation can increase reading load. | Design inference; no measured misunderstanding or correction rate is claimed. |
| V3 · NARROW | The flow still risked making users manage the process instead of the edit. | Narrow the task to object / region, preserve constraints, candidate comparison, and apply / undo / history. | A shorter decision path may reduce workflow burden, but range understanding and recovery still need testing. | Current design direction; no usability result is claimed. |

## Core interaction contract

1. Select the object or region to change.
2. Set priority-preserve constraints such as structure, windows, furniture, floor, lighting, and other objects.
3. Compare generated candidates and read the visible change summary.
4. Apply, undo, reject, or revisit the decision through history.

The proposed division of responsibility is:

- AI recognizes objects and spatial relationships, adapts references, generates candidates, and organizes differences.
- The user confirms scope, target change, preserve constraints, comparison choice, and final apply / undo / rejection.

## Visual evidence

### V1 · START

![V1 · START](../assets/v1-start.png)

The screen exposes a broad workflow and candidate set. Its value is process visibility; its risk is making the user manage too many intermediate states.

### V2 · EXPOSE

![V2 · EXPOSE](../assets/v2-expose.png)

The screen moves explanation closer to the decision: reference adaptation, extracted object, generation scope, and preserve constraints become visible before generation.

### V3 · NARROW

![V3 · NARROW](../assets/v3-narrow.png)

The screen keeps the room canvas central and makes change, preserve, compare, apply, undo, and history explicit. It is a product direction, not a working image-generation interface.

## What remains unvalidated

- Whether “change + keep” is natural for interior-editing users.
- Whether the canvas entry is more direct than a text-first or hybrid entry.
- Whether the change summary helps users compare candidates.
- Whether users can understand the edit boundary and recover from a wrong application.
- Steps, time, context switches, error points, satisfaction, and task success.
- Real model output quality and pixel-level stability outside the intended edit region.

The repository does not claim that any of these outcomes improved. The three images are static design evidence generated as visual material; no online model or runnable product is included.
