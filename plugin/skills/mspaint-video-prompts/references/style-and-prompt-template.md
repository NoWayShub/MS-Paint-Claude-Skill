# Master style block, character sheets, and the prompt template

## Contents
1. Master style block
2. Negative block
3. Character sheets
4. Per-image prompt template
5. Worked example
6. Prompt-writing notes

## 1. Master style block

Paste this at the start of every prompt, word for word:

```
Flat 2D cartoon illustration in a crude hand-drawn MS Paint style. Thick, slightly wobbly black outlines, solid flat colors with no gradients, no shading, no texture, no realistic lighting. Simple shapes, minimal background. 16:9 widescreen.
```

Why verbatim: the generator reads each prompt independently. Any change in wording shifts the look, and over 40-60 images the shifts add up to a video that looks inconsistent.

If the user wants a different look (watercolor, chalkboard, etc.), replace this block once, with their approval, and then keep the new one fixed.

## 2. Negative block

Paste this at the end of every prompt:

```
NO text, no letters, no numbers, no watermark, no realistic style, no 3D look, no gradients, no shadows.
```

Image models spell text badly, so labels, titles and captions are added later in the video editor. If a scene truly needs a sign or label, describe it as a blank sign.

## 3. Character sheets

Before writing any prompt, list every recurring subject and write one fixed description for each. Include:

- Body shape and relative size
- Exact colors (e.g. "mustard-yellow body, dark-green back plates")
- Face: eye style, expression default
- Distinctive features that make it recognizable
- Outline: "thick black outline"

Put the sheets at the top of the output file, and paste each one verbatim into the SUBJECT line of every prompt where that character appears. Don't shorten it in later prompts.

Example sheet:

```
Triceratops: a chunky, round-bellied dinosaur with olive-green skin, a lighter cream belly, three short horns (one on the nose, two above the eyes) colored cream, a wide bony frill behind the head colored orange, two small dot eyes with a calm expression, thick black outline.
```

One-off subjects (a single fern, a random rock) don't need a sheet.

## 4. Per-image prompt template

Order matters. Put the most important things first, because image models give more weight to the start of a prompt.

```
[MASTER STYLE BLOCK]

SCENE: <setting, background colors, ground, sky/water, mood. Say what is NOT in the background so it stays simple.>

SUBJECT: <character sheet(s) pasted verbatim, plus what they are doing and their expression/pose.>

CAMERA: <shot size + angle + how the viewer should feel, e.g. "Low angle medium shot, as if the viewer is on the ground looking up, so the animal feels huge.">

POSITION: <where each subject sits in the frame (left/center/right, top/bottom), how much of the frame it fills as a percentage, which way it faces, foreground vs background elements, where empty space is left.>

DOODLES: <small white or colored hand-drawn accents: stars, sparkles, "!" mark, motion lines, sweat drops. Say how many and where. "None" is allowed.>

[NEGATIVE BLOCK]
```

Aim for about 150-250 words per prompt. Detail is welcome as long as the key things stay near the top. Never drop sections to make a prompt shorter; if a prompt feels too long, cut repeated adjectives, not information.

## 5. Worked example

Line (0:12 - 0:17): "An octopus has three hearts, and its blood is blue."

```
Flat 2D cartoon illustration in a crude hand-drawn MS Paint style. Thick, slightly wobbly black outlines, solid flat colors with no gradients, no shading, no texture, no realistic lighting. Simple shapes, minimal background. 16:9 widescreen.

SCENE: Underwater seabed. The background is a plain flat blue ocean, and the bottom 15% of the frame is a flat pale-yellow sand strip with a gently wavy top edge. Nothing else in the background.

SUBJECT: A cute purple octopus with a round head, light-purple suckers on its arms, and two small dot eyes with a calm, curious expression. The body has a thick black outline.

CAMERA: Eye-level medium shot, as if the viewer is sitting on the seabed looking straight at the octopus. Slight low angle so the octopus feels a bit big and friendly.

POSITION: The octopus sits in the center-right of the frame, taking up about 55% of the width. It faces left, toward the viewer. One arm curls up toward the center of the frame, holding a single red strawberry with a green leaf top. The strawberry is clearly visible and sits in the middle of the frame. The left third of the frame is empty blue water.

DOODLES: Three small white hand-drawn stars and two short white sparkle lines above the strawberry. No other decorations.

NO text, no letters, no watermark, no realistic style, no 3D look, no gradients.
```

This prompt was tested by a user in Google Flow and gave the intended flat MS Paint look.

## 6. Prompt-writing notes

- **Position in percentages and directions** ("center-right, about 55% of the width, facing left") works better than vague words ("nicely placed").
- **One clear subject per image.** Crowded frames break the flat simple look and make characters drift.
- **Leave deliberate empty space.** The editor will slowly zoom or pan on each image, and space also lets the user add text overlays later.
- **Concrete over abstract.** For abstract lines ("this took millions of years"), design a visual metaphor: a long row of tiny calendars, a very tall stack of rocks, a clock with many hands.
- **Scale and comparison images**: show the two things side by side in the same frame, with the size difference stated in the position line ("the human is about one-tenth of the dinosaur's height").
- **Maps, charts, timelines**: avoid. They need text, which the generator can't render. Replace with a visual that conveys the same idea without labels.
- **Accuracy**: draw only what is true to the script. If the script says a dinosaur ate ferns, put ferns in the scene, and don't add features the animal didn't have.
