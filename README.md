# H3 Prompt Composer

**Version 5.11.1**

A free, standalone prompt-building tool for **MiniMax H3 video generation**, designed primarily for use with **ComfyUI**.

H3 Prompt Composer turns plain-language creative choices into structured H3 prompts. Instead of manually remembering reference syntax, subject numbering, audio mapping, shot structure, timing rules, and camera terminology, you build the scene through a browser-based interface and the Composer assembles the prompt for you.

The application is a **single HTML file**. There is nothing to install, no account is required, and it runs locally in a modern web browser.

---

## What It Does

H3 Prompt Composer supports the main MiniMax H3 generation modes:

- **T2VA** — text-to-video
- **I2VA** — first-frame / image-to-video
- **FL2VA** — first-frame to last-frame
- **L2VA** — generate toward a specified final frame
- **Ref2VA** — multi-reference generation using characters, environments, pictures, video, and audio references

For reference-heavy workflows, the Composer can help manage:

- Character and subject references
- Multi-view environment references
- Voice references and automatic subject-to-voice mapping
- Picture and video reference roles
- Character height / scale references
- Multiple Generations within one project
- Appearance continuity between Generations
- Multiple Shots within a Generation
- Timed Action Beats
- Dialogue and performance direction
- Camera framing, viewpoint, movement, timing, focus, and lens behavior
- Overall soundscape
- Non-diegetic music
- Prompt-length and reference validation
- Common prompt conflicts and continuity issues

The Composer generates the appropriate H3 prompt structure automatically based on the selected mode.

---

## Quick Start

1. Download `H3_Prompt_Composer_V5_11_1.html`.
2. Open it in a modern browser such as Chrome, Edge, or Firefox.
3. Choose the H3 mode you are using.
4. Set your target duration and visual style.
5. For Ref2VA projects, add the Subjects and references connected to your ComfyUI workflow.
6. Build your Generation using one or more Shots.
7. Add camera behavior, actions, dialogue, timing, sound, and music as needed.
8. Check the **Prompt Check** panel for errors or warnings.
9. Click **Copy Prompt** and paste the result into the corresponding H3 conditioning node in ComfyUI.

No installation is required.

---

## A Useful Mental Model

The Composer separates an H3 project into three timeline levels:

### Generation

One complete H3 generation request / output.

A project can contain multiple Generations so you can develop a sequence while carrying useful continuity forward.

### Shot

One continuous camera setup inside a Generation.

Create another Shot when there is an actual cut, transition, or change to a new camera view.

### Timed Action Beat

A timed action window inside a continuous Shot.

Use Timed Action Beats when actions need specific pacing but the camera does **not** cut.

For example, a single 10-second Shot might contain:

- 0–5 seconds: Character folds clothing into a suitcase.
- 5–10 seconds: Character closes the suitcase and carries it toward the door.

That remains one Shot.

---

## Ref2VA Reference Management

Ref2VA is intended for projects using character sheets, environment images, voices, performance videos, editing references, or other multi-reference workflows.

The Composer distinguishes between several different kinds of reference use.

### Subjects

A Subject is a reusable visible element such as:

- Character
- Creature
- Vehicle
- Prop
- Environment
- Other recurring visual element

Source images or videos that define a Subject are attached to that Subject.

### Standalone Pictures

Standalone Picture references are intended for images that have a separate job, such as:

- First-frame or last-frame anchors
- Composition anchors
- Storyboard / frame-planning references
- Wardrobe transfer
- Character height / scale references
- Environment-state references

This helps avoid unintentionally treating every source image as a target composition.

### Environments

Multiple views of the same location can be attached to a single Environment Subject.

The Composer treats those images as complementary views of one stable location while the Shot Builder determines the actual target framing.

### Voice References

An Audio reference can be bound to a Subject once.

When dialogue is created for that Subject, the Composer can resolve the correct voice automatically. If the Subject does not speak in the current Generation, an automatically managed voice reference can be bypassed so it does not consume an unnecessary logical H3 audio label.

---

## Camera Builder

The Camera Builder uses an **endpoint-first** workflow:

1. Define the **Start Frame**
2. Define the **End Frame**
3. Choose the **Camera Motion** that connects them

Controls can include:

- Shot size / framing
- Primary and secondary Subjects
- Horizontal viewpoint
- Camera height / vertical angle
- Composition
- Camera movement
- Movement timing
- Speed and range
- Stabilization / handheld character
- Lens perspective
- Depth of field
- Focus behavior
- Rack focus
- Custom movement instructions

The Composer also checks for some physically contradictory camera combinations rather than silently building conflicting instructions.

---

## Dialogue and Audio

Dialogue cards support:

- Speaker assignment
- Exact spoken words
- Language
- Delivery / performance direction
- Voice-reference resolution
- Off-screen or voice-over behavior
- Actions that occur immediately after a spoken line

The Composer generates H3 dialogue formatting and speaker IDs automatically.

---

## Video Reference Workflows

The Composer includes guided setups for several common Ref2VA video workflows, including:

### Insert Subject Into Existing Footage

Insert a generated Subject into an existing source video while preserving the original plate and camera behavior.

### Background Replacement + Relighting

Keep a filmed Subject while replacing the existing background with a new environment and integrating the Subject into the new scene through matching light, color, and environment interaction.

### Performance + Camera Transfer

Use a source video as a performance and/or camera-motion reference while applying that performance to the target Subject.

---

## Continuity Between Generations

A project can contain multiple Generations.

Creating a **New Generation** carries forward useful continuity such as:

- Base soundscape
- Music choice
- Supported Subject appearance state

Generation-specific extra sounds are intentionally reset.

**Duplicate Generation** can be used when you want to start from the same Shots and settings and create a variation.

Supported character Subjects can also maintain reusable appearance states so wardrobe or physical changes can persist through a sequence without manually rebuilding the character description every time.

---

## Prompt Check

The built-in Prompt Check looks for common problems before you copy the prompt.

Messages are grouped into:

- **Error** — something that should be corrected
- **Warning** — a possible conflict or risky instruction
- **Info** — guidance or optimization suggestions

Checks include things such as:

- Undefined or stale reference labels
- Invalid reference assignments
- Voice references bound incorrectly
- Conflicting camera instructions
- Reference-count limits
- Prompt-length limits
- Timing conflicts
- Duplicate or unnecessary reference use

Prompt Check is intended as a guardrail, not as a replacement for creative judgment.

---

## Saving Projects

The Composer automatically saves the active project locally in your browser.

You can also save a project as a JSON file and reopen it later.

Because projects are stored locally, clearing browser site data or changing browsers may remove the browser's autosaved copy. Use **Save Project** when you want a portable backup.

---

## Privacy and Security

H3 Prompt Composer is designed to run locally.

### The V5.11.1 build:

- Does **not** require an account
- Does **not** require installation
- Does **not** require an internet connection
- Does **not** load remote JavaScript libraries
- Does **not** load remote stylesheets
- Does **not** send prompts or project information to an external server
- Does **not** use `fetch`, XMLHttpRequest, WebSockets, or other network-request code
- Does **not** use `eval()` or dynamically execute downloaded code

The complete application source is contained in the HTML file and can be inspected directly in this repository.

The application does use normal browser features for its local functionality:

- **localStorage** for browser autosave / restore
- **Clipboard access** when you press **Copy Prompt**
- **FileReader** when you explicitly open a saved project JSON file
- Browser-generated local downloads when you save a project

The Composer does **not** load your ComfyUI images, videos, or audio files. It describes how reference inputs that are already connected in ComfyUI should be interpreted by H3.

---

## Documentation

Two guides are included with the release:

### Full User Guide

`H3_Prompt_Composer_V5_11_1_User_Guide.pdf`

A detailed reference covering the complete Composer workflow, reference management, Generations, Shots, Timed Action Beats, Camera Builder, dialogue, video-reference workflows, sound, continuity, saving, troubleshooting, and more.

### Illustrated User Guide

`H3_Prompt_Composer_V5_11_1_Illustrated_User_Guide.pdf`

A shorter visual guide intended to get new users oriented quickly with screenshots and workflow examples.

If you are new to the Composer, the Illustrated User Guide is a good place to start.

---

## Built-In Examples

The Composer includes example projects that can be loaded directly from the interface, including:

- Full reference scene
- Insert a Subject into existing footage
- Background replacement and relighting
- Performance and camera transfer
- Simple text-to-video shot

These are useful both as tutorials and as starting points for new projects.

---

## What the Composer Does Not Do

H3 Prompt Composer is a **prompt authoring and organization tool**.

It does not:

- Run MiniMax H3 itself
- Connect directly to ComfyUI
- Upload or process your source media
- Replace ComfyUI reference inputs
- Guarantee that H3 will follow every instruction exactly
- Replace experimentation with reference selection, prompting, seeds, or generation settings

The Composer helps create clearer, more internally consistent prompts. The final result is still generated by the underlying video model.

---

## Recommended Workflow

For complex Ref2VA work:

1. Give each reference **one clear job**.
2. Define reusable Subjects first.
3. Treat environment views as references to the location rather than target framing unless you explicitly need a frame anchor.
4. Use a new Shot only for a real camera cut or transition.
5. Use Timed Action Beats for pacing inside a continuous Shot.
6. Bind voices to Subjects once and let the Composer resolve them automatically.
7. Use the Camera Builder to define where the shot starts and ends before selecting movement.
8. Read Prompt Check before every generation.
9. Start simple and add controls only when they solve a specific problem.

---

## Version

Current release:

**H3 Prompt Composer V5.11.1**

---

## Disclaimer

H3 Prompt Composer is an independent community tool and is not an official MiniMax or ComfyUI product.

It is designed around MiniMax H3 prompting conventions and workflows and may need to evolve as the model, documentation, or community workflows change.

---

## Feedback

If you find a bug, confusing behavior, or an H3 prompting case the Composer does not handle well, feel free to open a GitHub Issue with:

- What you were trying to create
- The mode you were using
- The relevant reference setup
- The generated prompt, if possible
- What you expected to happen
- What happened instead

Clear examples make problems much easier to reproduce and improve.

---

**H3 Prompt Composer V5.11.1**  
Standalone HTML • Local browser tool • Built for MiniMax H3 workflows
