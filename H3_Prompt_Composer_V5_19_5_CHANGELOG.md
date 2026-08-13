# H3 Prompt Composer V5.19.5

V5.19.5 is a final project-save polish release built directly from V5.19.4. It intentionally leaves the established H3 prompt grammar, reference relationships, Prompt Check rules, Prompt Coach behavior, Camera Builder output, AI Setup schema, and six built-in workflow prompts unchanged.

## Project Save As

- **Save .json…** now uses the browser's native `showSaveFilePicker()` flow when available.
- The save picker receives the existing versioned JSON filename as its suggested name and starts in Documents on first use.
- A dedicated picker ID allows Chromium browsers to remember the last-used directory for subsequent project saves.
- The user can rename the project and choose the destination folder before the JSON is written.
- Canceling the Save As dialog exits cleanly without writing or downloading anything.
- Browsers without the File System Access save picker keep the previous `<a download>` behavior as a compatibility fallback.
- If the native picker exists but cannot be used in the current browser context, the same fallback preserves project export rather than failing.

## Compatibility and Migration

- New local-storage keys: `h3_prompt_composer_v5_19_5` and `h3_prompt_composer_v5_19_5_backup`.
- V5.19.4 project state is copied forward automatically on first launch when V5.19.5 has no saved state yet.
- V5.19.4 Restore Previous backups are included in the fallback chain.
- Existing earlier-version migration fallbacks remain intact.

## Prompt-output regression

The following built-in examples were compared directly between V5.19.4 and V5.19.5:

- Full reference scene
- Insert a subject into existing footage
- Background replacement + relighting
- Performance + camera transfer
- Continue an existing video
- Simple text-to-video shot

All six generated prompts are **byte-for-byte identical** between V5.19.4 and V5.19.5.

## Final audit

- Inline JavaScript passes `node --check`.
- No duplicate HTML IDs were found.
- Clean Chromium loading produced no page exceptions or internal application errors.
- Layout regression passed at 390, 1280, 1366, 1440, 1920, and 2560 px viewport widths with no document or column horizontal overflow.
- Native Save As was exercised with a stubbed file handle: the expected versioned filename, JSON contents, writable close, picker ID, and cancel behavior all passed.
- Compatibility fallback was exercised both with the native API absent and with a non-cancel picker failure.
- Static offline/security scan found no `fetch()`, XMLHttpRequest, WebSocket, EventSource, `sendBeacon`, `eval()`, dynamic `new Function`, or embedded HTTP/HTTPS dependency.
- Source diff against V5.19.4 was reviewed: changes are limited to version/migration bookkeeping, the Save control, and the Save As/fallback implementation.

## Scope

V5.19.5 does not add another feature layer. It is intended as the polished publication candidate after the V5.19.4 community-UX pass.
