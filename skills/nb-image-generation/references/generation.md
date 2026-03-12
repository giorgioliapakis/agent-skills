# Image Generation Workflows

Detailed guidance for creating images, icons, patterns, stories, and diagrams.

## Writing effective prompts

Gemini responds best to structured, descriptive prompts. Include:

- **Subject**: what's in the image
- **Style**: photorealistic, watercolor, flat illustration, 3D render, sketch, pixel art
- **Composition**: close-up, wide shot, overhead view, centered, rule of thirds
- **Lighting**: natural light, golden hour, studio lighting, dramatic shadows, neon
- **Mood**: warm, cold, energetic, calm, mysterious, playful

**Example - vague prompt:**
```bash
nb generate "a cat" --json
```

**Example - detailed prompt:**
```bash
nb generate "a tabby cat sitting on a windowsill, golden hour sunlight streaming in, watercolor style, warm tones, soft focus background of a garden" --json
```

The more specific you are, the closer the output matches your intent.

## Generating multiple variations

Use `-n` to generate up to 8 variations in one call:

```bash
nb generate "minimalist logo for a coffee brand" -n 4 --aspect 1:1 --json
```

Each variation interprets the prompt differently. Useful for exploring directions before refining.

## Controlling aspect ratio and resolution

Common aspect ratios and their use cases:

| Ratio | Use case |
|-------|----------|
| 1:1 | Icons, social media posts, profile images |
| 16:9 | Presentations, desktop wallpapers, YouTube thumbnails |
| 9:16 | Mobile screens, Instagram stories, TikTok |
| 4:3 | Blog images, product photos |
| 3:2 | Photography, print |
| 21:9 | Ultrawide banners, hero images |

Resolution options: 512px (fast drafts), 1K (default, good balance), 2K (high quality), 4K (maximum detail, slower).

## Reproducible output

Use `--seed` to get the same output from the same prompt:

```bash
nb generate "mountain landscape at dawn" --seed 42 --json
nb generate "mountain landscape at dawn" --seed 42 --json  # same result
```

Useful when you like a composition but want to tweak the prompt while keeping the overall structure.

## Icons and favicons

Use `nb icon` for app icons, logos, and favicons:

```bash
nb icon "minimalist calendar app icon, flat design, blue gradient" --aspect 1:1 --resolution 1K --json
```

For multi-size icon sets, generate at the highest resolution and downscale:

```bash
nb icon "rocket ship logo" --aspect 1:1 --resolution 4K --json
```

## Seamless patterns

`nb pattern` generates tileable patterns for backgrounds and textures:

```bash
nb pattern "subtle geometric triangles, navy and gold" --aspect 1:1 --json
nb pattern "tropical leaves watercolor" --resolution 2K --json
```

## Visual sequences (stories)

`nb story` generates a multi-frame sequence where each image represents a step:

```bash
nb story "making a latte from bean to cup" --steps 6 --json
```

Good for: tutorials, process documentation, storyboards, onboarding flows.

## Diagrams

`nb diagram` generates technical visualizations:

```bash
nb diagram "microservices architecture with API gateway, auth service, and database" --json
nb diagram "user signup flow with email verification" --json
```

The output is an image, not editable vector. Use for quick visualization, not production architecture docs.

## Thinking mode

For complex prompts that need more reasoning (detailed scenes, specific compositions):

```bash
nb generate "isometric city block with a park, shops, and apartments" --thinking high --json
```

Levels: `off` (fastest), `low`, `high` (most reasoning). Note: `medium` is NOT supported.
