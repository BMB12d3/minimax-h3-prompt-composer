# H3 Prompt Composer V5.18.8

V5.18.8 is a pre-publication bug-fix and polish release built from a full headless audit of V5.18.7. It preserves the V5.18.7 interface, reference-routing model, output section structure, and AI Setup schema (v4). No prompt sections, reference labels, or workflow behaviors were redesigned.

## Fixed

- **Release identity labels** now consistently show V5.18.8 in the browser-tab title, visible header, and embedded source banner.
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
- Scanned all 460 functions and every inline event handler: no remaining orphaned functions are reachable from the UI, and no handler references an undefined function.

## Known non-changes (documented for the audit record)

- `aiSetupInstructionsLegacy` and `validateAIImportLegacy` remain in the file as unreferenced dead code. They are harmless and retained for reference; remove in a future cleanup if desired.
- The edit-workflow instruction prose (continuation handoff, insert-subject integration, background-relight) intentionally repeats key constraints across subject_definitions, retention_analysis, and detailed_description. This costs roughly 60-120 words per workflow prompt. It was left untouched because that prose has been validated against H3; a future release could consolidate it if generations remain stable with shorter phrasing.
- The V5.18.6 PDF guides remain workflow-compatible. Their AI Setup screenshot may still show the former **Preview import** label instead of **Re-check import**; no other illustrated workflow changed in V5.18.8.
