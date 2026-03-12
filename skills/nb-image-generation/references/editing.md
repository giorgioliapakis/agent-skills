# Editing and Restoration Workflows

Detailed guidance for modifying existing images, batch operations, and using reference images.

## Single file editing

Pass an image file and describe the change:

```bash
nb edit photo.png "make it black and white" --json
nb edit headshot.jpg "remove the background, replace with solid white" --json
nb edit product.png "add a subtle drop shadow" --json
```

The CLI searches for input files in: current directory, `./images/`, `./input/`, `./nanobanana-output/`, `~/Downloads/`, `~/Desktop/`.

## Batch editing

Apply the same edit to multiple files at once:

```bash
nb edit *.png "add a vintage sepia filter" --json
nb edit photo1.jpg photo2.jpg photo3.jpg "crop to square, center the subject" --json
```

Each file gets processed independently with the same instruction.

## Reference images

Use `--ref` to pass additional images as context. The model uses these for style, composition, or content reference:

```bash
# Style transfer: make the target look like the reference
nb edit --ref style-reference.png target.png "apply this visual style" --json

# Compositing: combine elements from multiple references
nb edit --ref logo.png --ref background.png "place the logo centered on this background" --json

# Brand consistency: use existing assets as reference
nb edit --ref brand-example.png new-asset.png "match the color palette and typography style" --json
```

`--ref` is repeatable - pass as many reference images as needed.

## Photo restoration

`nb restore` is optimized for repair and enhancement:

```bash
# Colorize a black and white photo
nb restore old-bw-photo.png "colorize naturally" --json

# Fix damage
nb restore scratched-photo.png "remove scratches and repair damage" --json

# Enhance low quality
nb restore blurry-photo.png "enhance sharpness and detail" --json

# Combined restoration
nb restore vintage-photo.png "colorize, remove scratches, enhance detail" --json
```

Multiple files can be restored in one call:

```bash
nb restore scan1.png scan2.png scan3.png "restore and enhance these photos" --json
```

## Output placement

Always specify an output directory with `-o` to keep files organized:

```bash
nb edit photo.png "crop to 16:9" -o ./processed/ --json
nb restore old-photo.png "enhance" -o ./restored/ --json
```

Without `-o`, files go to the default `nanobanana-output/` directory.

## Iterative editing workflow

For complex edits, work in iterations:

1. Make the first edit:
   ```bash
   nb edit source.png "remove background" -o ./iterations/ --json
   ```

2. Review the output, then refine:
   ```bash
   nb edit ./iterations/source.png "clean up edges around the hair" -o ./iterations/ --json
   ```

3. Continue until satisfied. Use `--seed` if you want to try different prompts on the same base.

## Known limitations

- Text rendering in generated/edited images may have artifacts - treat as drafts if typography matters
- Complex compositing (multiple overlapping elements) works best with clear, specific prompts
- The model may not perfectly reproduce specific brand fonts or logos - use `--ref` to get closer
- Very large files may take longer to process
