---
description: Generate a wide or portrait tech stack card image prompt for the current repository using StackShot.
argument-hint: [style] [wide|portrait]
---

Use the StackShot skill to scan the current repository and generate a tech stack card image prompt.

If `$ARGUMENTS` is provided, parse it for a visual style and image format.

Supported styles are:

- `default`
- `dark glass`
- `neon`
- `minimal`
- `brutalist`
- `cyberpunk`
- `terminal`

Supported formats are:

- `wide`
- `portrait`

If no style is provided, ask the user which style they want. If no format is provided, ask whether they want `wide` or `portrait` before producing the final prompt.

Follow the StackShot skill workflow exactly: collect repository metadata, infer the project stack, count files/LOC/tests, derive the language breakdown, inspect repo styling when `default` is selected, then output only the final image-generation prompt.
