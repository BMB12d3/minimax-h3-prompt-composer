# H3 Prompt Composer V5.18.8

V5.18.8 is a pre-publication bug-fix and polish release built from a full headless audit of V5.18.7. It preserves the V5.18.7 interface, reference-routing model, output section structure, and AI Setup schema (v4). No prompt sections, reference labels, or workflow behaviors were redesigned.

## Fixed

- **Copy all generations** now works. The button previously called a function that did not exist in the file, so clicking it threw a silent `ReferenceError` and copied nothing (present in V5.18.6 and V5.18.7). It now copies every Generation's prompt in order, separated by `===== Generation N =====` headers, with a single combined error-count confirmation before copying.
- **Base-mode Shot 1 capitalization.** When a style is set, the first content clause after the style comma is now lowercased regardless of whether it comes from the opening-state or the action field. `Live-action, cinematic, The baker opens...` is now `Live-action, cinematic, the baker opens...`, matching the MiniMax base-guide format.
- **Sentence-start capitalization for user prose.** Opening-state and action text that starts a new sentence mid-prompt is now capitalized even when typed lowercase, so `...before sunrise. he places a loaf` becomes `...before sunrise. He places a loaf.` Reference labels and quoted text at the start of a sentence are unaffected.
- **Automatic summary grammar.** A single previous-generation continuity picture now reads "preserves assigned previous-generation blocking or scene state" instead of "preserve."
- **Restore previous** now includes the V5.18.7 and V5.18.6 backup keys in its fallback chain. Both keys were previously skipped, so the button could report "no previous project backup" for users arriving from those versions after the first-launch migration window.

## Prompt Check

- A standalone Picture reference (continuity frame, composition anchor, etc.) that occupies the same physical Picture slot as an **active Environment view in the same Generation** now raises a clear warning instead of a soft info note. One connected image cannot simultaneously be a clean Environment view and a separate reference image, and the previous behavior let the same `<Picture N>` label carry two contradictory definitions into the prompt.

## AI Project Setup

- The **Preview import** button is renamed **Re-check import**, with a tooltip explaining that pasted JSON is checked automatically and the button exists to re-run validation after the Composer project changes (for example, after Generation 1 has been imported and an append JSON's validity depends on the current project).
- The import help text now states explicitly that the JSON's `operation` field decides the outcome: `replace_project` replaces the whole project, while `append_generations` (produced when the LLM is given **Copy next-Generation context**) merges the new Generation(s) into the current project.
- When a `replace_project` JSON is previewed while a meaningful project already exists, the preview adds a notice pointing to **Copy next-Generation context** as the way to append instead of replace.

## Fixed (critical)

- **Custom camera override crash.** Any Generation containing a Shot with the Custom camera override enabled crashed with "Maximum call stack size exceeded" the moment it was rendered or its prompt was built. The POV scan inside the custom-camera path (`cameraCustomPovUids`) routed back through the per-Generation active-reference machinery while that machinery was still computing itself, creating infinite recursion. Because rendering died before the Generation bar repainted, the symptom looked like haunted UI: Generation tabs that would not switch, Copy prompt silently copying nothing, and delete confirmations naming a different Generation than the one highlighted. The scan now uses stable library-scoped Subject labels, which are recursion-free and produce identical POV detection. This bug also exists in V5.18.7; it triggers whenever a custom-camera Shot with text exists in the active Generation.
- **Re-entrancy guards.** The two cached derived-state builders (active-reference set and per-Generation Audio label map) now detect re-entry during their own computation and return a safe empty transient instead of overflowing the stack, so no future code path can reproduce this class of hard crash.

## Fixed (second audit pass)

- **Frame Grabber "Copy filename" was broken.** It called a nonexistent `copyText` function (leftover from an old clipboard-helper rename, broken in V5.18.7 as well), so clicking it threw a silent error and copied nothing. It now uses the shared clipboard helper and is verified against the real clipboard.
- **Environment view-name typing threw on every keystroke.** The view-name input's handler called a nonexistent `saveSoon()` after storing the value (also present in V5.18.7). The stored name survived, but the prompt preview never refreshed and an error fired per keystroke. It now calls `buildOnly()`, matching the sibling view-role handler, so the prompt and autosave update live while typing.
- **UI version labels updated.** The page title, header logo, and script banner still read V5.18.7; all now read V5.18.8.
- **Dead code removed.** The two orphaned legacy functions (`aiSetupInstructionsLegacy`, `validateAIImportLegacy`) noted in the first audit have been deleted.

## Reliability

- **Visible error reporting.** Any uncaught internal error now shows a dismissible red bar at the bottom of the window with the failure location and a **Copy error report** button (app version, project stats, and the last 20 errors with 30-line stack traces). Previously, an exception thrown while rendering a Generation failed silently: the internal selection changed but the tabs, output pane, and copy buttons froze on stale state — which could make Generation tabs appear unclickable and make the delete confirmation name a different Generation than the one highlighted.
- **Resilient rendering.** Each interface section now renders independently. If one Generation's data makes one section fail, the Generation bar, shot list, and all other sections still update, so healthy Generations remain fully selectable and editable.
- **Loud copy failures.** If a prompt cannot be built, **Copy prompt** and **Copy all generations** now explain why in an alert instead of silently copying nothing; Copy all substitutes a clear placeholder for the failing Generation and continues.

## Compatibility

- V5.18.8 uses new autosave and backup keys and imports V5.18.7 (or, failing that, V5.18.6) local state on first launch.
- The AI Setup interchange format and schema_version 4 are unchanged. Existing replace and append JSON documents import identically.
- The six Ref2VA sections, three base-mode fields, and all mode headers are unchanged.
- All six built-in examples produce byte-identical prompts relative to V5.18.7 and pass Prompt Check with no errors or warnings.

## Verification

- Headless audit executed all six built-in examples, all five modes (T2VA, I2VA, FL2VA, L2VA, Ref2VA), the AI Setup replace and append flows, and V5.18.6/V5.18.7 state migration with zero console or page errors.
- Copy all generations verified against the real browser clipboard with a two-Generation project.
- The base-mode capitalization fixes verified against the MiniMax base-guide Shot 1 format.
- The Environment-slot collision warning verified with an active Environment on Pictures 5-6 plus a continuity Picture on slot 5 in the same Generation.
- Scanned all functions and every inline event handler: no orphaned functions remain, and no handler references an undefined function.
- Second audit pass: AST-accurate call-graph cycle detection (including function-reference callback edges) reports zero cycles; a whole-script sweep for calls to undefined identifiers reports zero after the two fixes above; 230+ prompt builds across the full camera-type × timing × endpoint matrix, custom-camera POV in all six workflows, eight dialogue variants, all five modes, and multi-Generation stress produced zero exceptions and zero malformed-output findings (no stray tokens, unbalanced <d> tags, double spaces, or punctuation faults); 850 UI clicks, 149 text-input events, and 27 checkbox toggles across four project states produced zero errors; AI-import edge cases (unknown asset IDs, invalid enums, negative duration, markdown-fenced JSON, legacy schema v3) all degrade gracefully.

## Known non-changes (documented for the audit record)

- The edit-workflow instruction prose (continuation handoff, insert-subject integration, background-relight) intentionally repeats key constraints across subject_definitions, retention_analysis, and detailed_description. This costs roughly 60-120 words per workflow prompt. It was left untouched because that prose has been validated against H3; a future release could consolidate it if generations remain stable with shorter phrasing.
