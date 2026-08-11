# H3 Prompt Composer V5.18.5

## Purpose
V5.18.5 clarifies and formalizes the difference between persistent project-media identity and temporary physical H3/ComfyUI Picture-slot routing, especially for projects that reuse Picture inputs across multiple Environments and Generations.

## Core routing model
- A library image has a persistent semantic identity: e.g. Jane character sheet, Jungle Clearing wide view, Broken Bridge ramp detail.
- `<Picture N>` is a physical ComfyUI input used by the active Generation, not a permanent global image ID.
- Fixed/pinned Subject references may keep stable slots (for example Jane/John/T-Rex/Jeep at Pictures 1-4).
- Environment views may reuse the remaining legal Picture inputs independently for each Environment.
- The built-in AI example now demonstrates:
  - Jungle Clearing -> Pictures 5-6
  - Jungle Road -> Picture 5
  - Broken Bridge -> Pictures 5-7
- Reusing Picture 5 across different Environment nodes is valid because those Environment assets are alternatives and are not intended to be connected simultaneously.
- Multiple views inside the *same* Environment still require different physical slots because they are used together.

## AI instruction changes
The copied AI Setup instructions now explicitly tell the LLM:
- Do not interpret upload order, conversational labels such as "picture 10", or ENV/View numbering as physical H3 Picture slots.
- Only an intentional `P##` prefix or an explicit statement such as "ComfyUI Picture 3" declares a fixed physical Picture slot.
- Treat H3's Picture limit as a simultaneous-input limit, not a limit on the number of logical images that may exist across a multi-Generation project.
- Keep explicitly pinned Subject slots stable unless the user says otherwise.
- Route each Environment independently into the lowest reusable legal Picture inputs that do not collide with fixed references needed in that Generation.
- Do not discard an Environment view merely because it was the 10th/11th/etc. source image supplied to the LLM; remap the logical view into a legal reusable slot.
- Preserve an out-of-range slot conflict only when the user explicitly demanded that physical slot.

## User-facing media naming guidance
The AI Setup modal now distinguishes fixed physical-slot names from slot-independent project-media names.

Recommended examples:
- `P01_Jane_CHARACTER_SHEET.png` — intentionally pinned to physical Picture 1
- `P02_John_CHARACTER_SHEET.png`
- `ENV01_JungleClearing_V01_WIDE.png` — logical Environment view; no permanent Picture slot implied
- `ENV01_JungleClearing_V02_SHED_SIDE.png`
- `ENV02_JungleRoad_V01_WIDE.png`
- `ENV03_BrokenBridge_V01_WIDE.png`
- `ENV03_BrokenBridge_V02_APPROACH.png`
- `ENV03_BrokenBridge_V03_RAMP_DETAIL.png`
- `G01_JaneJohn_CONT_BLOCKING.png` — add a `P##` prefix only after/if its physical slot is deliberately fixed

## Environment-node UI changes
- Environment nodes now state directly that their selected Picture numbers are routing for that Environment, not permanent project-image IDs.
- The help text explicitly gives the 5-6 / 5 / 5-7 reuse example.
- Each selected Environment view can now have a stable human-readable view name in addition to its contribution role.
- Stable view names are preserved through AI import/export (`assets.environments[].pictures[].name`).

## AI interchange / validation
- Schema remains v4 for backward compatibility.
- `assets.environments[].pictures[]` now supports an optional `name` field alongside `slot` and `contribution`.
- The validator explicitly allows the same Picture slot to be reused by different Environments.
- The validator now catches an accidental duplicate Picture slot within one Environment.
- Existing 5.18.4 projects are **not automatically rewired** on migration. Their current routing is preserved so a deliberate user wiring choice is never silently changed.

## Regression validation
- JavaScript syntax: PASS (`node --check`).
- Whole-script evaluation without browser boot: PASS.
- Built-in AI starter template: 0 validation errors / 0 warnings; max Picture slot 7.
- Starter Environment routing imported correctly as 5-6 / 5 / 5-7.
- Environment view names and contribution roles survived import and export.
- Named-Environment AI interchange round trip: byte-identical.
- Same Picture number reused across different Environments: accepted with 0 errors.
- Duplicate Picture number inside one Environment: correctly rejected.
- All six built-in workflow prompts are byte-for-byte identical to V5.18.4, confirming the prompt-generation engine was not altered:
  - Full reference scene
  - Insert subject
  - Background replace + relight
  - Performance + camera transfer
  - Continuation
  - T2VA
- All six built-in workflows: 0 Prompt Check errors / 0 warnings.
- Hidden/non-printing control characters: 0.
- Duplicate top-level function declarations: 0.
- Network/dynamic-code scan remains clean: no fetch/XHR/WebSocket/EventSource/sendBeacon/eval/new Function.

## Existing imported Jungle project
The previously returned AI JSON remains structurally valid in V5.18.5 and imports successfully. Because V5.18.5 does not silently rewrite existing projects, its old Environment routing remains:
- Jungle Clearing -> Pictures 5-6
- Jungle Road -> Picture 7
- Broken Bridge -> Pictures 8-9

For the user's intended ComfyUI workflow, those Environment nodes should be manually changed to:
- Jungle Clearing -> Pictures 5-6
- Jungle Road -> Picture 5
- Broken Bridge -> Pictures 5-7

Future AI-generated setups using V5.18.5 instructions should understand this reusable routing model directly.
