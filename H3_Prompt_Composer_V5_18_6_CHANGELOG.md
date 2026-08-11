# H3 Prompt Composer V5.18.6

V5.18.6 is a focused audit-and-documentation release. It preserves the V5.18.5 reusable Environment-routing model while correcting issues found in an independent review of the app, README, and both manuals.

## Application changes

- Fixed AI Setup's media-naming table so long filenames no longer overlap their explanations. The filename column sizes to its content on wide screens and collapses cleanly on narrow screens.
- Hardened the AI Setup naming grid further so filenames wrap inside a bounded column at intermediate widths.
- Reworked collapsed reference-card headers so long Subject and Environment names wrap inside the card while collapse and remove controls remain reachable. The left column no longer creates a horizontal scrollbar.
- Restored the missing V5.18.1 autosave and backup migration keys.
- Added the V5.18.5 autosave and backup keys to the V5.18.6 handoff chain.
- Improved style normalization for adjective-only modifiers. For example, `vintage film, grainy, desaturated` now becomes “The target video is in a vintage film style, with a grainy and desaturated look.”
- Added leading-style recognition for anime, film noir, stop-motion, hand-drawn, rotoscope, and oil painting.
- Treats any safe single-word style modifier as a visual descriptor, covering terms such as tactile, crisp, stark, clean, lush, neon, and somber.
- Rejects a non-string Environment-view `name` during AI import instead of round-tripping it as `[object Object]`.

## Documentation changes

- Rebuilt the full and illustrated guides with more targeted, current UI views.
- Removed duplicated illustrated-guide captions and reduced unnecessary forced page breaks.
- Kept headings with their related content to avoid orphan headings and large empty page regions.
- Extended heading pagination protection to blue subheadings and replaced reused generic workspace captures with targeted Camera, appearance, scale, dialogue, workflow, and Check-panel views.
- Corrected the README's Connected ComfyUI Inputs image link.
- Documented the exact output structure: base modes use `integrated_multimodal_description`; Ref2VA uses `subject_definitions`, `summary`, `retention_analysis`, `detailed_description`, `overall_soundscape`, and `non_diegetic_music`.
- Documented the 4–15 second request range and 24 fps `17n+5` frame normalization, including the 10.00-second to 243-frame / 10.13-second example.
- Clarified that V5.18.5's byte-for-byte comparison applied specifically to V5.18.4 built-in workflow output, not to every earlier 5.18.x prose revision.

## Reviewed and intentionally retained

The camera-stability vocabulary noted in the audit remains intentional. Terms such as stabilization behavior, motion continuity, and camera endpoint constraints are useful operational guidance even when they are not enumerated in the compact reference guide.

## Compatibility

- Standalone local HTML; no installation required.
- Schema version remains 4.
- Existing project JSON remains migratable.
- Existing Environment routing is not silently rewritten.

## Verification

- Inline JavaScript parses successfully.
- Style-normalization regression cases pass.
- Autosave and backup chains include every V5.18.x release key from V5.18.0 through V5.18.6.
- The standalone file contains no external runtime dependency or network request API.
- Both PDFs were rendered to page images and checked for page count, text extraction, repeated long captions, and visual layout.
