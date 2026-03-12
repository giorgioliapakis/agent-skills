---
name: nb-image-generation
description: |
  Generate and edit images via the nanobanana CLI (Gemini image models).
  Use this skill whenever the user asks to create images, edit photos, restore old images,
  generate icons, create patterns, produce visual sequences, or make diagrams. Also trigger
  on casual requests like "make me an image", "touch this up", "create a logo", or "visualize this".
  Requires: npm install -g @giorgioliapakis/nanobanana
---

# NB Image Generation

Image generation and editing via the `nanobanana` (or `nb`) CLI, powered by Google's Gemini image models.

## Prerequisites

```bash
npm install -g @giorgioliapakis/nanobanana
```

## Auth

Check if credentials are stored:

```bash
nb login --api-key YOUR_GEMINI_API_KEY
```

Or use an environment variable:

```bash
export GEMINI_API_KEY="YOUR_KEY"
nb generate "test" --api-key "$GEMINI_API_KEY"
```

Once `nb login` is run, the key is stored and `--api-key` is no longer needed.

## Choosing the right command

| Need | Command | When to use |
|------|---------|-------------|
| Create an image from scratch | `nb generate` | Text-to-image, any subject or style |
| Modify an existing image | `nb edit` | Change colors, add elements, restyle, batch edits |
| Fix or enhance old/damaged images | `nb restore` | Upscale, colorize, repair artifacts |
| App icons, logos, favicons | `nb icon` | Automatically frames prompt as icon generation |
| Seamless tiling patterns | `nb pattern` | Backgrounds, textures, wallpapers |
| Multi-frame visual sequence | `nb story` | Step-by-step tutorials, storyboards, process flows |
| Technical diagrams | `nb diagram` | Architecture diagrams, flowcharts, system visualizations |

## Commands

### nb generate

```bash
nb generate "a watercolor painting of a fox" --json
nb generate "coffee shop interior" -n 3 --aspect 16:9 --json
```

Creates images from text prompts. Use `-n` for multiple variations (1-8).

### nb edit

```bash
# Single file
nb edit photo.png "make it black and white" --json

# Batch: same edit to multiple files
nb edit *.png "add a vintage filter" --json

# Multi-reference: combine images as context
nb edit --ref logo.png --ref style.png "create a banner combining these" --json
```

The `--ref` flag passes reference images for style matching or compositing. Repeatable.

### nb restore

```bash
nb restore old-photo.png "enhance and colorize" --json
```

Enhances or repairs damaged, old, or low-quality images.

### nb icon

```bash
nb icon "rocket ship logo" --aspect 1:1 --json
```

Shortcut that prepends "Generate an icon:" to your prompt. Use `--aspect 1:1` for square icons.

### nb pattern

```bash
nb pattern "geometric hexagons" --aspect 1:1 --json
```

Shortcut that prepends "Generate a seamless pattern:" to your prompt.

### nb story

```bash
nb story "a seed growing into a tree" --steps 4 --json
nb story "how to make coffee" -n 6 --json
```

Generates a sequence of images. Each gets "step N of M" appended. Use `-n/--steps` to control frame count (2-8).

### nb diagram

```bash
nb diagram "CI/CD pipeline with GitHub Actions" --json
```

Shortcut that prepends "Generate a diagram:" to your prompt.

## Global options

| Option | Description | Default |
|--------|-------------|---------|
| `--aspect <ratio>` | Aspect ratio (1:1, 16:9, 9:16, 4:3, 3:2, 21:9) | - |
| `--resolution <res>` | Image resolution: 512px, 1K, 2K, 4K | 1K |
| `--seed <n>` | Seed for reproducible output | - |
| `--temperature <n>` | Sampling temperature (0.0-2.0) | model default |
| `--thinking <level>` | Thinking mode: off, low, high (not medium) | off |
| `-o, --output <dir>` | Output directory | nanobanana-output/ |
| `--json` | Structured JSON output | - |
| `--api-key <key>` | API key override | - |
| `--preview` | Open result in system viewer | - |

## Execution guidelines

1. Always use `--json` for structured output - parse the `files` array for output paths.
2. Always use `-o <dir>` to place output in a meaningful location, not the default `nanobanana-output/`.
3. Avoid `--preview` unless the user explicitly asks to open files.
4. Preserve user constraints for style, aspect ratio, resolution, and count.
5. For reproducibility, use `--seed <number>` when users want consistent reruns.
6. `--thinking medium` is NOT supported - use off, low, or high only.

## JSON output contract

```json
{
  "success": true,
  "message": "Successfully generated 1 image variation(s)",
  "files": ["/absolute/path/to/output.png"]
}
```

On failure, `success` is false and an `error` field contains the details.

## Workflow references

For detailed workflows and prompting tips, read the relevant reference:

| Task | Reference |
|------|-----------|
| Image generation, prompting techniques, style control | [references/generation.md](references/generation.md) |
| Editing, restoration, batch operations, reference images | [references/editing.md](references/editing.md) |

Read only the reference you need for the current task.
