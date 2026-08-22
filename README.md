# H3 Prompt Composer

**Version 5.37.14**

A free, standalone prompt-building app for **MiniMax H3** video generation and reference-guided image workflows.

**One HTML file · no installation · runs locally in your browser**

![H3 Prompt Composer V5.37.1 overview](assets/v5371-overview.png)

## Video tutorial

[![Watch the H3 Prompt Composer V5.37.1 tutorial](https://img.youtube.com/vi/Aywx3Sf5Yk0/hqdefault.jpg)](https://youtu.be/Aywx3Sf5Yk0)

**[Watch the V5.37.1 tutorial on YouTube](https://youtu.be/Aywx3Sf5Yk0)**

## What it does

H3 Prompt Composer turns your filmmaking choices into structured H3 prompts. You work with visual controls for references, Shots, timing, camera movement, dialogue, continuity, editing, and sound; the app assembles the correct prompt structure and checks it before generation.

- Builds prompts for **T2VA, I2VA, FL2VA, L2VA, Ref2VA, and reference-guided images**.
- Organizes reusable characters, environments, pictures, videos, voices, continuity frames, and placement guides.
- Maps physical ComfyUI inputs with a guided setup instead of making you manage labels by hand.
- Creates multiple named Environment locations from a reusable Picture-input bank.
- Provides a Camera Builder and visual camera-path planner.
- Includes guided workflows for insertion, replacement, targeted edits, relighting, performance transfer, and continuation.
- Handles timed Shots, action beats, dialogue, voiceover, scene transitions, cutoffs, ambience, and music.
- Checks prompt structure, timing, references, audio, camera, continuity, and input routing.
- Runs offline and keeps project data in your browser unless you choose to save or export it.

## Features and interface

### Guided references and camera planning

| Guided Reference Setup | Visual Camera Planner |
| --- | --- |
| ![Shared Environment input bank and reusable locations](assets/v5371-guided-reference.png) | ![Visual Camera Planner](assets/v5371-visual-planner.png) |
| Map connected Picture, Video, and Audio inputs. Create named locations and assign each one its own subset of the shared Environment bank. | Place timed camera positions, choose straight or arc movement, and generate one natural camera instruction. |

### Editing and prompt checking

| Guided Targeted Edit | Prompt Check |
| --- | --- |
| ![Targeted Edit camera setup](assets/v5371-targeted-edit-camera.png) | ![Prompt Check pass](assets/v5371-prompt-check.png) |
| Define the requested change, protect the source footage, and choose one camera-authoring method. | Catch structural, timing, reference, dialogue, audio, camera, continuity, and mapping conflicts before generation. |

### Project utilities

| Local Frame Grabber | AI Project Setup |
| --- | --- |
| ![Local Frame Grabber](assets/v5371-frame-grabber.png) | ![AI Project Setup](assets/v5371-ai-setup.png) |
| Capture native-resolution PNG frames from local video and give them purpose-readable filenames. | Export structured project context for an external LLM and validate returned project JSON before import. |

### Reference-guided image mode

![Reference-guided image mode](assets/v5371-image-mode.png)

Build a one-frame edit or composite prompt with explicit reference roles, requested changes, protected elements, and output requirements.

## Get started

1. Download **[H3_Prompt_Composer_V5_37_14.html](H3_Prompt_Composer_V5_37_14.html)**.
2. Open it in Chrome, Edge, Firefox, or another modern browser.
3. Choose a mode, describe the Generation, and add only the references you need.
4. Review **Check**, then click **Copy prompt** and paste the result into your H3 workflow.

The Composer describes media already connected to H3 or ComfyUI. It does not upload reference files or run the model itself.

## Supported workflows

| Mode | Use it for |
| --- | --- |
| **T2VA** | Text-to-video generation |
| **I2VA** | Starting from a required first image |
| **FL2VA** | Connecting required first and last frames |
| **L2VA** | Generating toward a required final image |
| **Ref2VA** | Full-reference generation, editing, continuation, and audio workflows |
| **Image** | A reference-guided still-image edit or composite |

## Current release

V5.37.14 carries forward the V5.37.1 workflow and documentation with updated camera prompting and Guided Reference Setup behavior.

See the **[V5.37.1 changelog](H3_Prompt_Composer_V5_37_1_CHANGELOG.md)** for the full release notes.

## Manuals and downloads

- **[Full User Guide](H3_Prompt_Composer_V5_37_1_User_Guide.pdf)** — complete workflow and field reference.
- **[Illustrated User Guide](H3_Prompt_Composer_V5_37_1_Illustrated_User_Guide.pdf)** — visual quick start and feature tour.
- **[SHA-256 checksum](H3_Prompt_Composer_V5_37_14_SHA256.txt)** — verifies the standalone HTML file.

## Local and private by design

The app is self-contained and has no external scripts, stylesheets, accounts, or server dependency. It makes no network requests during normal use. Browser features are used only for local storage, clipboard copy, user-selected project/media files, saves, exports, and local frame capture.

## Disclaimer

H3 Prompt Composer is an independent community tool and is not an official MiniMax or ComfyUI product. A clean Prompt Check cannot guarantee model compliance; results still depend on the model, workflow settings, and reference quality.
