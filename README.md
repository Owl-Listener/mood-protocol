# mood-protocol

**A visual-to-semantic bridge for AI-assisted design.**

Designers think in images. AI agents think in text. `mood.md` is a protocol that connects the two.

Drop your moodboard images into a folder — screenshots of annotated Figma canvases, colour palettes, typography specimens, spatial references, things you love, things you hate — and generate a structured `mood.md` that any AI agent can use for design direction.

## Why this exists

We can write `SKILL.md` files to tell agents *how* to build things. But we have no equivalent for telling them *what it should feel like*. Design intent is fundamentally visual, and right now that gets lost in translation.

`mood.md` is the missing counterpart:

| File | Purpose |
|------|---------|
| `SKILL.md` | "Here's how to do things" (procedural) |
| `mood.md` | "Here's what it should feel like" (perceptual) |

Together, they give an agent both craft knowledge and aesthetic direction — the full picture of what a designer brings to a project.

## Quick start (no setup required)

The simplest way to generate a `mood.md` — no code, no API keys, no terminal.

### 1. Screenshot your moodboard

Export your annotated Figma canvas as a PNG, or screenshot your Pinterest/Miro board. Sticky notes, labels, and spatial groupings are all valuable — the AI reads everything visible.

### 2. Upload and prompt

Open the AI you already use — [claude.ai](https://claude.ai), [gemini.google.com](https://gemini.google.com), [chatgpt.com](https://chatgpt.com) — upload your images, and paste the prompt from **[PROMPT.md](PROMPT.md)**.

### 3. Save the output

Copy the response into a file called `mood.md` in your project root. Done.

That's it. Three steps, zero setup, works right now.

---

## Automated version (for repeat use)

If you want to run this from the command line without copy-pasting, there's a Python script that does it in one command.

### Install (pick your model)

```bash
# For Claude
pip install anthropic
export ANTHROPIC_API_KEY=your-key-here

# For Gemini
pip install google-genai
export GEMINI_API_KEY=your-key-here
```

### Create a mood folder and generate

```
my-project/
  mood/
    your-images-here.png
    notes.md              ← optional designer annotations
  mood.md                 ← generated
```

Drop your reference images into the `mood/` folder, then:

```bash
python generate_mood.py --name "Editorial Warmth"

# Or use Gemini instead
python generate_mood.py --model gemini --name "Editorial Warmth"
```

**Anti-references** (things you don't want) are signalled by prefixing filenames with `not-` or `anti-`:
```
mood/
  warm-editorial-layout.png
  colour-palette.png
  not-corporate-dashboard.png    ← anti-reference
```

### Options

```bash
python generate_mood.py                            # scans ./mood/ → ./mood.md (uses Claude)
python generate_mood.py --model gemini             # use Gemini instead
python generate_mood.py --input ./brand-refs       # custom input folder
python generate_mood.py --output ./src/design      # custom output location
python generate_mood.py --name "Dark Mode Variant"  # name your mood
```

## What mood.md looks like

A generated `mood.md` contains structured, actionable design direction:

- **Essence** — 2-3 sentences capturing the overall feeling
- **Colour** — temperature, palette (with hex values), contrast, saturation
- **Typography** — character, weight distribution, suggested pairings
- **Space & Layout** — rhythm, grid character, scale relationships
- **Texture & Material** — surface quality, material references
- **Emotional Register** — how someone should *feel*
- **Design Principles** — extracted from the moodboard
- **Anti-References** — what this explicitly is NOT
- **Agent Instructions** — actionable paragraph for any AI agent

## Using mood.md with agents

Once generated, `mood.md` works with any AI assistant or coding agent. Place it in your project root alongside your code, and reference it in prompts:

**With Claude Code:**
```
Read mood.md and apply its direction to the landing page components.
```

**With Cursor / Copilot / any agent:**
```
Before styling this component, read mood.md for the project's visual direction.
```

**Multiple moods per project:**
```
my-project/
  moods/
    brand/
      mood/
        ...images...
      mood.md
    dark-mode/
      mood/
        ...images...
      mood.md
    onboarding/
      mood/
        ...images...
      mood.md
```

## Works with any design tool

This protocol is tool-agnostic. Your moodboard images can come from:

- **Figma** — export a frame as PNG
- **Stitch** — screenshot or export
- **Miro / FigJam** — screenshot your board
- **Pinterest** — save images to a folder
- **Are.na** — download your channel
- **Your phone** — photograph a physical moodboard
- **Anywhere** — if it's an image, it works

## Works with any AI model

The output is just markdown. Any model that can read text can use it — Claude, Gemini, GPT, Llama, whatever you prefer.

The generator script supports Claude and Gemini out of the box. Adding another vision backend is straightforward — contributions welcome.

## Philosophy

- **Designer-native** — formalises what designers already do, no new workflow to learn
- **Model-agnostic** — the output works with any AI
- **Tool-agnostic** — the input works from any design tool
- **Composable** — multiple moods per project, each a different direction
- **Versionable** — it's a text file, it lives in git
- **Open** — MIT licensed, free to use, adapt, and extend

## Contributing

This is an early-stage protocol. Contributions welcome:

- **Alternative vision backends** — Gemini, GPT-4o, local models
- **Framework integrations** — Claude Code slash commands, Cursor rules, etc.
- **Figma plugin** — one-click export from a Figma frame
- **Format extensions** — motion, sound, interaction mood dimensions
- **Example mood files** — share your generated moods

## License

MIT

---

*mood-protocol was created by [MC Dean](https://substack.com/@marieclairedean) as part of ongoing work on [Percolates](https://marieclairedean.substack.com) — exploring design, AI, and the craft of making things well.*
