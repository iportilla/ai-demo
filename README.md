# image-demo Notebook

This workspace contains a Jupyter notebook that demonstrates image generation workflows with the OpenAI Images API. The notebook walks through three common operations:

- Generating an image from a text prompt
- Creating prompt-based "variations" of the generated image
- Editing part of an existing image with a mask

The main notebook is `/Users/ivanp/Downloads/demo/image-demo.ipynb`.

## What The Notebook Covers

The notebook is organized into these sections:

1. Setup
2. Image generation with `client.images.generate(...)`
3. Variation-style outputs by regenerating the same prompt multiple times
4. Image editing with `client.images.edit(...)`

The notebook saves outputs into the `images/` folder in the workspace root.

## Requirements

- Python 3.9+
- An OpenAI API key with access to image generation

Python packages used by the notebook:

- `openai`
- `python-dotenv`
- `requests`
- `Pillow`

Install them with:

```bash
pip install openai python-dotenv requests Pillow
```

## Configure Your API Key

The notebook loads environment variables from a local `.env` file:

```env
OPENAI_API_KEY=your_api_key_here
```

It also falls back to the shell environment if `OPENAI_API_KEY` is already exported.

## How To Run

1. Open `/Users/ivanp/Downloads/demo/image-demo.ipynb` in Jupyter or VS Code.
2. Select a Python kernel.
3. Install the required packages if they are not already available in that environment.
4. Create the `.env` file with your API key.
5. Run the notebook from top to bottom.

## Output Files

Running the notebook can create files like these under `images/`:

- `generated_image.png`
- `variation_image_0.png`
- `variation_image_1.png`
- `bottom_half_mask.png`
- `edited_image.png`

## Notes About Variations

The notebook includes a "Variations" section, but it does not call the legacy variation endpoint directly. Instead, it simulates variations by generating multiple images from the same prompt with `dall-e-3`.

That means the outputs are best understood as alternate generations from the same prompt, not strict image variations derived from a source PNG.

## Models Used In The Notebook

- `dall-e-3` for image generation
- `dall-e-2` for image editing

This matches current API support shown in the notebook cells.

## Workspace Contents

- `/Users/ivanp/Downloads/demo/image-demo.ipynb`: main image API demo notebook
- `/Users/ivanp/Downloads/demo/CNN-101.ipynb`: separate notebook not required for this demo
- `/Users/ivanp/Downloads/demo/images/`: generated outputs and masks

## Troubleshooting

- If authentication fails, verify `OPENAI_API_KEY` is set correctly.
- If imports fail, install the missing packages in the active notebook kernel.
- If image downloads fail, confirm the API response returned a valid image URL and that network access is available.
- If the edit step fails, make sure the generated source image and mask both exist and are valid PNG files.