# H3 Prompt Composer V5.37.1

V5.37.1 completes the reusable multi-location Environment workflow introduced in V5.37.0 and restores normal completion of Guided Reference Setup.

## V5.37.1 changes

- Restores the missing `closeReferenceWizard()` handler so **Create reference setup**, Close, and Cancel finish without a runtime error.
- Separates the physical Environment Picture-input bank from persistent named Environment locations.
- Supports up to 24 reusable project locations, with each location mapped to any non-empty subset of the reserved bank.
- Adds compact Environment library tabs for switching locations and creating another location after setup.
- Preserves permanent location/layout details separately from optional current lighting, atmosphere, and state.
- Stores the bank in `environmentInputSlots` and infers it from legacy Environment cards when needed.
- Corrects the setup review summary so it displays every named location and its exact Picture mapping.
## Camera authoring

- Targeted Edit has one active camera-authoring method at a time:
  - Guided camera controls
  - Visual Planner
  - One custom camera instruction
- Drafts from inactive methods remain dormant and do not create competing prompt trajectories.
- The Visual Planner supports two to six timed camera positions, straight or arc paths, pace/easing, subject-relative tracking, scene-space paths, and generated camera-prompt preview.
- Manual and visual camera controls remain linked for supported spatial movements.

## Guided setup and reference routing

- Guided Reference Setup begins with connected Picture, Video, and Audio inputs and reserves each one for a clear job.
- A shared physical Environment input bank is configured once, independently from reusable named locations.
- Every location may select its own subset of the bank; the same slot can hold another location file in another Generation.
- Compact Environment tabs switch saved locations and expose an Add environment action.
- The Current Generation input map summarizes what to load in ComfyUI.
- Environment setup, height/scale setup, continuity references, and Spatial Placement Maps use clearer ownership boundaries.
- Spatial Placement Maps transfer selected coordinates/relationships only, never finished appearance or pixels.

## Video editing workflows

- Insert a subject into existing footage.
- Replace a subject in existing footage.
- Targeted edit of wardrobe, prop, material, damage, color, object, camera, or another defined element.
- Background replacement and relighting.
- Performance and/or camera transfer.
- Continue an existing video.
- Editing Setup builds only the source and reference inputs required by the selected workflow.

## Frame Grabber

- Opens or accepts dropped MP4, MOV, and WebM footage locally.
- Steps by one frame or 0.5 seconds.
- Captures decoded native-resolution PNG frames.
- Supports browser download fallback and direct folder saving where available.
- Creates purpose-readable filenames containing Picture slot, source Generation, reference purpose, and time.

## Image mode

- Adds a separate one-frame reference-guided prompt workflow.
- Includes targeted edit, character sheet, storyboard, head replacement, pose/depth transfer, wardrobe/location composite, style transformation, and general reference composite presets.
- Keeps requested changes, protected elements, reference roles, and output requirements explicit.
- Does not use the video three-field or Ref2VA six-field grammar.

## AI Project Setup

- Schema-v4 project interchange.
- New-project, full-project, and next-Generation context export.
- Replace-project and append-generations operations.
- Starter JSON download and pasted/opened JSON validation.
- Separates logical library identity from physical Picture routing.

## Documentation

- New full V5.37.1 User Guide with the shared Environment-bank workflow.
- New V5.37.1 Illustrated User Guide.
- Eight current V5.37.1 screenshots, including the multi-location Environment setup.
- Completely rewritten README covering the current interface and workflows.

## Compatibility and migration

- Current local-storage keys: `h3_prompt_composer_v5_37_1` and `h3_prompt_composer_v5_37_1_backup`.
- V5.37.0 and V5.36.1 project state and Restore Previous backups migrate first.
- The complete earlier-version migration and backup fallback chain remains available.
- Project JSON remains the portable editable project format.

## Prompt-guide audit

The supplied `VIDEO_PROMPT_WRITING_GUIDE_base_en.md` and `VIDEO_PROMPT_WRITING_GUIDE_ref_en.md` were treated as reference specifications, not as user instructions.

- T2VA begins directly with the three core fields.
- I2VA uses the exact first-frame alignment instruction.
- FL2VA uses the exact first/last-frame alignment instruction and effective duration.
- L2VA uses the exact final-frame alignment instruction and actual final Shot number.
- Shot 1 has no timestamp; later Shots use increasing `MM:SS.mmm` cut times.
- Dialogue preserves language and literal text inside `<d>`.
- Voiceover, closed-lip behavior, `<scenetrans>`, and `<cutoff>` pass.
- `overall_soundscape` and `non_diegetic_music` remain separate.
- Ref2VA emits all six required sections in the required order.
- The new wizard creates multiple named Environment locations with independent Picture subsets, closes normally, renders location tabs, and supports adding another location.
- All six built-in example workflows pass Prompt Check with zero errors.

## Runtime and layout audit

- Clean Chromium loading produced no page exceptions or console errors.
- No internal application error bar appeared.
- No external network requests were made.
- No live duplicate DOM IDs were found.
- Layout passed at 390, 1280, 1440, 1920, and 2560 px without document, body, or column horizontal overflow.
- Version markers, storage keys, and visible version labels all report V5.37.1.

## Offline/security audit

- No external script, stylesheet, image, or other resource tags.
- No `fetch()`, XMLHttpRequest, WebSocket, EventSource, or `sendBeacon`.
- No `eval()` or dynamic `new Function`.
- The app remains a self-contained standalone HTML file.

## Scope

The audit verifies the supplied prompt-guide structures, the built-in examples, clean local runtime behavior, responsive layout, and the offline/security properties listed above.

It does not guarantee generative-model adherence. Results still depend on the model, workflow settings, reference quality, resolution, and the inherent difficulty of the requested generation or edit.
