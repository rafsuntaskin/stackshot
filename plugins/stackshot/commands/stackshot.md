---
description: Generate a 1200x630 tech stack card image prompt for the current repository using StackShot.
argument-hint: [style]
---

Use the StackShot skill to scan the current repository and generate a 1200x630 tech stack card image prompt.

If `$ARGUMENTS` is provided, treat it as the requested visual style. Supported styles are:

- `default`
- `dark glass`
- `neon`
- `minimal`
- `brutalist`
- `cyberpunk`
- `terminal`

If no style is provided, ask the user which style they want before producing the final prompt.

Follow the StackShot skill workflow exactly: collect repository metadata, infer the project stack, count files/LOC/tests, derive the language breakdown, inspect repo styling when `default` is selected, then output only the final image-generation prompt.
