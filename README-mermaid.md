# image-demo Notebook Diagrams

This document complements the main README with Mermaid charts for the image demo notebook in [image-demo.ipynb](/Users/ivanp/Downloads/demo/image-demo.ipynb).

## Notebook Flow

```mermaid
flowchart TD
    A[Open image-demo.ipynb] --> B[Install and import packages]
    B --> C[Load .env and read OPENAI_API_KEY]
    C --> D[Create OpenAI client]
    D --> E[Ensure images directory exists]
    E --> F[Generate base image with dall-e-3]
    F --> G[Download and save generated_image.png]
    G --> H[Display generated image]
    H --> I[Generate two prompt-based alternate images]
    I --> J[Save variation_image_0.png and variation_image_1.png]
    J --> K[Create bottom_half_mask.png]
    K --> L[Edit original image with dall-e-2]
    L --> M[Save edited_image.png]
    M --> N[Display original and edited outputs]
```

## Runtime Interaction

```mermaid
sequenceDiagram
    participant U as User
    participant N as Notebook
    participant E as Environment
    participant O as OpenAI Images API
    participant FS as images/

    U->>N: Run setup cells
    N->>E: Load .env
    E-->>N: OPENAI_API_KEY
    N->>FS: Create images directory if missing

    U->>N: Run generation cells
    N->>O: images.generate(prompt, model=dall-e-3)
    O-->>N: Image URL
    N->>FS: Save generated_image.png

    U->>N: Run variation cells
    loop Two alternate generations
        N->>O: images.generate(same prompt, model=dall-e-3)
        O-->>N: Image URL
    end
    N->>FS: Save variation_image_0.png and variation_image_1.png

    U->>N: Run edit cells
    N->>FS: Save bottom_half_mask.png
    N->>O: images.edit(source image, mask, prompt, model=dall-e-2)
    O-->>N: Edited image URL
    N->>FS: Save edited_image.png
```

## Artifact Map

```mermaid
graph LR
    A[.env] --> B[OPENAI_API_KEY]
    B --> C[OpenAI client]
    C --> D[Generate base image]
    D --> E[generated_image.png]
    E --> F[Create mask]
    F --> G[bottom_half_mask.png]
    E --> H[Edit request]
    G --> H
    H --> I[edited_image.png]
    D --> J[Repeat prompt-based generations]
    J --> K[variation_image_0.png]
    J --> L[variation_image_1.png]
```

## Section-to-File Relationship

```mermaid
flowchart LR
    A[Setup] --> B[.env]
    A --> C[images/]
    D[Generation] --> E[generated_image.png]
    F[Variation-style outputs] --> G[variation_image_0.png]
    F --> H[variation_image_1.png]
    I[Mask creation] --> J[bottom_half_mask.png]
    K[Edit] --> L[edited_image.png]
```

## Notes

- The notebook's "Variations" section is implemented as repeated prompt-based generations, not as a call to the removed legacy variation endpoint.
- The current workspace already contains [generated_image.png](/Users/ivanp/Downloads/demo/images/generated_image.png).
- Additional files appear only after their corresponding notebook sections are run.