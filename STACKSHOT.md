---
name: stackshot
description: Generate a wide or portrait image-generation prompt for a repository tech stack card by scanning project metadata, source files, tools, tests, language breakdown, and optional brand styling. Use when the user asks for a StackShot, tech stack card, repository card, social preview card, or image prompt summarizing a codebase.
---

# StackShot

Scan the current repository and generate a structured image-generation prompt for a tech stack card.

Collect repository facts using available file-reading, search, manifest-parsing, or code-inspection tools. Prefer structured project metadata over guessing, and avoid inventing exact values when the repository does not support them.

## Collect

1. Project name:
   - Prefer the `name` field from the primary manifest when available.
   - Otherwise use the repository or folder name.
2. File count:
   - Count source and project files.
   - Exclude dependency, build, cache, generated, and VCS directories such as `node_modules`, `.git`, `dist`, `vendor`, `__pycache__`, `.next`, `build`, and `coverage`.
3. Lines of code:
   - Count meaningful source lines across common implementation files such as TypeScript, JavaScript, Python, Go, Rust, PHP, Ruby, Java, Kotlin, Swift, and C#.
   - Use the same exclusions as file count.
   - Avoid counting lockfiles, generated files, minified assets, compiled output, and vendored code.
4. Primary framework and language:
   - Infer from manifests, dependency files, config files, entry points, and dominant source files.
   - If multiple apps exist, choose the main user-facing app or the largest active code area.
5. Key tools or dependencies:
   - List up to 4 recognizable technologies.
   - Prefer the primary framework first, then important runtime, database, styling, testing, build, or deployment tools.
6. Test count:
   - Count files that are clearly tests, such as `*.test.*`, `*.spec.*`, `test_*.py`, `*_test.go`, or files inside conventional test directories.
7. Language breakdown:
   - Identify the top 3 languages by approximate source LOC.
   - Return percentages that sum roughly to 100%.

## Derive

- Format LOC compactly, such as `12.4k` or `1.2M`.
- Count the number of detected programming languages.
- Write a one-line subtitle describing the project, such as `Next.js e-commerce platform` or `FastAPI async microservice`.
- If a value cannot be determined confidently, use a conservative best-effort label such as `Unknown`, `Mixed`, or an approximate value.
- If the project name or subtitle is ambiguous, ask the user to confirm or provide the correct value before generating the final prompt.
- If any numeric value is `0`, omit that field from the final image-generation prompt instead of passing `0`.

## Ask For Style

Ask the user which style they want:

- `default` - infer the visual direction from the repository's own brand, design system, CSS, Tailwind theme, component library, or documentation.
- `dark glass` - deep dark background, frosted panels, glowing accents.
- `neon` - black background, vivid neon colors, high contrast.
- `minimal` - white or off-white, clean typography, monochrome.
- `brutalist` - stark high contrast, bold type, raw grid.
- `cyberpunk` - deep violet/electric, futuristic UI aesthetic.
- `terminal` - black background, monospace, green or amber phosphor.

If the user chooses `default`, inspect the repository for brand and design guidance before generating the final prompt. Look for sources such as global CSS, base styles, design tokens, CSS variables, theme files, Tailwind config, Sass/Less files, component styles, Storybook files, UI package config, public assets, logos, screenshots, README docs, brand docs, or design-system documentation.

Use those findings to describe the image style generically. Do not mention implementation filenames in the final image prompt unless they are part of the brand name. If no clear brand or theme guidance exists, fall back to a clean modern developer-card aesthetic.

## Ask For Format

Ask the user which image format they want:

- `wide` - 1200x630, best for social preview cards, GitHub README images, and landscape sharing.
- `portrait` - 900x1600, best for mobile-first Facebook feed images, stories-style previews, and narrow vertical sharing.

If the user already requested a format, use it without asking again.

## Final Output

After the user chooses a style and format, output only this block with all placeholders replaced:

```text
Generate a [IMAGE_WIDTH]x[IMAGE_HEIGHT] pixel tech stack card image in [STYLE_TYPE] style.

DATA:
- Project: [PROJECT_NAME]
- Subtitle: [SUBTITLE]
- Primary framework: [PRIMARY_FRAMEWORK]
- Tools: [TOOL_1], [TOOL_2], [TOOL_3], [TOOL_4]
- Files: [FILES_COUNT]
- Lines of code: [LOC_FORMATTED]
- Languages: [LANG_COUNT]
- Tests: [TEST_COUNT]
- Language breakdown: [LANG_1] [PCT_1]%, [LANG_2] [PCT_2]%, [LANG_3] [PCT_3]%

Omit any DATA line whose value is zero, empty, or unavailable.

LAYOUT:
- Header: large bold project name + smaller subtitle below
- Badge row: pill-shaped tech badges, first one highlighted as primary
- Stats section: 4 stats (FILES / LOC / LANGUAGES / TESTS) with values prominent and labels small below
- Language bar: horizontal segmented bar with color per language + legend below
- Footer: small "Generated by StackShot" bottom-right

For wide format, use a compact landscape layout with the stats in a horizontal row. For portrait format, use a narrow mobile-card layout with stacked sections, a 2x2 stats grid, larger touch-friendly spacing, and clear safe margins so the card reads well in a Facebook mobile feed.

Let the color palette, typography weight, and visual treatment reflect the [STYLE_TYPE] aesthetic. Make it look like a premium developer social card.
```
