# Your agent is design-blind

You've been doing the work. You've written the SKILL.md files, set up the slash commands, built the multi-agent pipelines. Your AI can scaffold a React component in seconds. It can follow a design system. It can match your spacing tokens.

And the output still feels like it was made by a very competent stranger who has never seen the inside of your head.

Here's why. We've given agents procedural knowledge, how to do things, but we have no way of telling them what something should feel like. And for designers, that feeling is the whole job.

## The gap nobody's talking about

Think about how you actually work. Before you open Figma, before you write a single line of CSS, you've already built something in your mind. You've collected images, torn pages out of magazines (or their digital equivalent), pinned things to a board. You've grouped them, annotated them, drawn lines between them. You've written "YES this energy" on a sticky note next to a photograph of a bookshop at dusk.

That moodboard is the highest-bandwidth communication tool in your entire workflow. It carries colour temperature, spatial rhythm, typographic character, emotional register, material quality, and a dozen other signals that would take thousands of words to describe, and even then you'd lose the texture.

Now look at the tools we've built for agents. SKILL.md tells them how to write good CSS. CLAUDE.md tells them how to behave. Cursor rules tell them your preferences. All text. All procedural. All blind to the visual.

**There's no protocol for how things should feel.**

## Moodboards already exist. They just need a bridge.

The interesting thing is that designers already have the answer. You already curate visual direction. You already know how to communicate aesthetic intent through images. The problem is that this communication happens in Figma, on a canvas, in a spatial medium that agents cannot see.

So we built a bridge.

It's called **mood-protocol**, and the idea is almost embarrassingly simple. You take your moodboard, the one you've already made, the one with the sticky notes and the annotations and the spatial groupings, and you export it as an image. Drop it into a folder. Run one command. And a vision model reads everything, the images, the annotations, the relationships, the anti-references, and generates a structured `mood.md` that any agent can consume.

The output looks like a creative direction brief written by a design director who has deeply understood your intent. Colour palettes with hex values and semantic names. Typography character. Spatial rhythm. Emotional register. And crucially, a section called **Agent Instructions** that tells any AI exactly how to apply this mood when making design decisions.

## How it works

The workflow is deliberately simple, because the best tools disappear into what you're already doing.

**Step 1:** Create a moodboard however you normally do. Figma, Stitch, Miro, a folder of screenshots from Pinterest, a photograph of a physical board pinned to your wall. It doesn't matter.

**Step 2:** Export it. If you're working in Figma, the most powerful move is to screenshot your entire annotated canvas, sticky notes and all. The vision model reads everything visible, including your handwritten commentary. That spatial, annotated context is enormously valuable.

**Step 3:** Drop the images into a `/mood/` folder in your project. If you want, add a `notes.md` with any freeform thoughts: "I want this to feel like a Sunday morning magazine. NOT corporate. NOT glassmorphic."

**Step 4:** Run the command.

```
python generate_mood.py --name "Editorial Warmth"
```

That's it. Your `mood.md` is generated and ready.

It works with Claude or Gemini (just add `--model gemini`), and because the output is plain markdown, any agent can read it. Claude Code, Cursor, Copilot, whatever you use. The protocol is model-agnostic and tool-agnostic by design.

## What makes this interesting

You could look at this and think, okay, nice little utility. But I think something bigger is happening here.

We've spent the last year building increasingly sophisticated ways to give agents procedural knowledge. Skill files, system prompts, fine-tuned models. And that's necessary work. But procedural knowledge is only half of what a human expert brings to a problem.

The other half is perceptual. Taste. Judgment. The ability to look at something and know it's wrong before you can articulate why. Designers have cultivated this sense over years. It lives in their eyes, in their accumulated experience of what works and what doesn't, in the moodboards they curate and the anti-references they collect.

**We've been encoding the "how" and ignoring the "what it should feel like."**

`mood.md` is a small attempt to correct that. But the pattern is bigger than design. Musicians curate sonic references. Writers collect passages that carry the tone they're reaching for. Architects photograph spaces that embody the quality of light they want. Every creative discipline has its own version of the moodboard, a collection of perceptual references that guide decisions in ways that procedural instructions cannot capture.

If SKILL.md is the protocol for craft knowledge, then `mood.md` is the beginning of a protocol for aesthetic intent. And I think we're going to need a lot more protocols like it before agents can truly collaborate with creative humans rather than just executing instructions.

## The anti-reference might be the most important part

One thing I love about this approach is that it gives space for what you don't want. In design, knowing what to avoid is as valuable as knowing what to pursue. "NOT corporate dashboard" carries as much information as "warm editorial layout." Maybe more, because it closes off an entire territory of bad decisions.

You can prefix any filename with `not-` or `anti-` and the system treats it as a negative signal. "Here is what this is emphatically not." I haven't seen any other agent tool that handles this, and it's how designers actually think. We define spaces by their boundaries.

## Try it

The whole thing is open source. One Python script, no dependencies beyond the API you already use, works with any design tool.

You need images, a folder, and one command. That's it.

I built this because I kept running into the same wall. My agents could follow instructions beautifully and still produce work that felt generic, because they had no access to the visual direction in my head. The moodboard was right there on my Figma canvas. It just had no way to cross the bridge into the text-based world where agents live.

Now it does.

If you try it, I want to hear what happens. Did the output surprise you? Did agents produce noticeably different work when they had a mood file? What's missing from the format?

And if you're sitting there thinking about what other forms of human intelligence are currently invisible to agents, what other bridges we need to build, well. That's the conversation I want to be having.

Because we're still in the early days of teaching machines to see what we see. And the interesting work is in the translation.
