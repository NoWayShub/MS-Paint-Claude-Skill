---
name: mspaint-video-prompts
description: End-to-end workflow for faceless YouTube slideshow videos made of simple, flat, MS-Paint-style cartoon images (about one image every 3-8 seconds, with voiceover). Claude writes the narrator script (or uses the user's own), then, once the user shares voiceover timestamps, designs every image (camera angle, scene, character positions) and delivers complete copy-paste image prompts in a .txt file for Google Flow, Midjourney, DALL-E or similar tools. Use this skill whenever the user mentions faceless YouTube videos, slideshow-style videos, animated-looking photo videos, MS Paint or doodle style visuals, ElevenLabs voiceover plus images, scene-by-scene or timestamp-based image prompts, or wants a script and image prompts for any explainer, facts, story or history video, even if they don't name this style explicitly.
---

# MS-Paint-Style Slideshow Video: Script to Image Prompts

This skill turns a topic (or a ready script) into a full set of image prompts for a slideshow-style video. The look is a crude, flat, hand-drawn cartoon style with thick wobbly outlines and solid colors. Each image stays on screen for a few seconds while a voiceover plays.

Claude cannot generate images itself. The deliverable is prompts that the user pastes into an image tool (Google Flow, Midjourney, DALL-E, etc.). Don't claim specific features of those tools (reference images, saved styles, aspect-ratio menus) as verified; tell the user to check what their tool offers.

The user's pipeline: topic -> script -> user records voiceover (usually ElevenLabs) -> user gives timestamps -> Claude designs each image and writes its prompt -> user generates images -> user edits in CapCut/DaVinci/Canva.

Reply in the language the user writes in (Hindi, Hinglish, English, etc.). The image prompts themselves are always written in English, because image models follow English prompts most reliably.

## Step 1: Ask with a poll first

Start with one `ask_user_input_v0` call (a tappable poll) instead of typing out questions. Write the question and option text in the user's own language. Skip any question the user has already answered in their message.

Ask these in a single call:

1. **Script source**: Claude writes the script from a topic / the user already has a script / the user has a rough idea and wants Claude to polish it
2. **Narration language**: Hindi / Hinglish (Roman script) / English / another language
3. **Video length**: about 2-3 min / about 5 min / about 8-10 min

The topic is free text, so don't make it a poll. If the user hasn't given one, ask for it in a plain message after the poll. If the user pasted their own script, skip the topic question.

After the poll answer, confirm the plan in one or two lines and move on. Don't re-ask what the poll already settled.

## Step 2: The script

Read `references/script-writing.md` before writing or editing a script.

- If the user supplied a script, don't rewrite it. Offer light fixes only (long sentences that will sound unnatural in a voiceover, unclear lines) and ask before changing anything.
- If Claude is writing it, keep facts accurate. If web search is available, verify specific claims (numbers, dates, names, "firsts") before putting them in the script. If a fact is uncertain or debated among experts, say so in the narration ("scientists think...") instead of stating it as settled.
- Write one idea per line so each line can become one image.

Deliver the script in chat, then tell the user what to do next: generate the voiceover, and send back timestamps (see Step 3).

## Step 3: Get the timestamps

Ask for timestamps in this shape, but accept any reasonable format:

```
0:00 - 0:04  Line text
0:04 - 0:09  Line text
```

If the user only gives total audio length plus the script, estimate timing from word count, tell them clearly that it's an estimate, and that real timestamps will give a better match between image and voice. Never present estimated times as exact.

## Step 4: Plan the images

- Aim for roughly one image per 5 seconds, but let the audio decide: short lines of 3-4 seconds can get their own image, and long lines (7-8 seconds or more) can be split into two images. Two very short lines can share one image.
- Make a compact plan first: number, time range, the line, and a one-line visual idea. Put this index at the top of the output file, and show only a brief summary in chat. Don't stop to ask for approval unless the user asked to approve the plan.
- Every image should show what the line is *about*, so the viewer understands it even with the sound off.

## Step 5: Lock the style and the characters

Read `references/style-and-prompt-template.md`. Two things must be identical across all prompts so the images look like one video:

- **Master style block**: copy it verbatim into every prompt.
- **Character sheets**: for every recurring character or creature, write one fixed description (colors, shape, size, face, distinctive features) and paste it verbatim into every prompt where that character appears. Do not paraphrase it between prompts, since small wording changes produce visibly different characters.

## Step 6: Design each image

Read `references/camera-guide.md`. For every image, decide deliberately (not by default):

1. **Camera angle and shot size**, and *why* it suits this line (emotion, scale, detail, surprise)
2. **Scene design**: setting, background, colors, mood
3. **Position design**: where each subject sits in the frame, how big it is, which way it faces, what's in the foreground and background, where empty space is left
4. **Doodles**: the small white sparkles, "!" marks, motion lines and similar hand-drawn accents that give this style its character. Keep them few and relevant.

Then check the sequence as a whole: don't use the same shot type more than twice in a row, and make sure the lighting/color story stays consistent across scenes of the same location.

Prompts must be complete and detailed. Don't shorten or drop sections to save space; if length is a problem, split the delivery into batches (see Step 7), not the prompts.

## Step 7: Deliver as a .txt file, in batches

Long prompts for 40-60+ images don't fit in one chat message and may not fit in one turn's output either. So:

1. Write the file with bash in **batches of about 10 prompts**, creating it first with the header (title, master style block, character sheets, image index), then appending each batch.
2. Use plain `.txt`, not .docx, so copy-paste carries no hidden formatting.
3. Use the entry format below so each prompt is self-contained and cleanly copyable.
4. Save to `/mnt/user-data/outputs/` and call `present_files`. Don't paste the full prompts into chat.
5. If the output limit is reached mid-way, tell the user exactly which image number was the last one written, and continue appending when they say "continue".

Entry format:

```
==================================================
IMAGE 07  |  0:32 - 0:38  (6s)
LINE: "the narrator's line for this image"
SHOT: low angle, medium shot. Why: makes the creature feel huge as the line talks about its size.
--------------- COPY PROMPT FROM HERE ---------------
<full self-contained prompt>
--------------- END PROMPT ---------------
```

The "SHOT ... Why" note sits outside the copy area, so the user can paste cleanly.

## Step 8: Wrap up

After the file is delivered, give the user a short note:

- Generate image 1 first and check the style before generating the rest; if it drifts, say so and the style block gets adjusted.
- Check the aspect ratio in their tool's own settings as well as in the prompt.
- Add any on-screen text in the video editor, not in the image (image models misspell text).
- Offer to rewrite any prompt whose generated image didn't match, and ask what went wrong so the template can improve.

## Quality checklist (run before delivering)

- Every timestamped line is covered by an image, with no gaps in the timeline.
- Master style block and character sheets are verbatim in every prompt that needs them.
- Important things (style, subject, position, camera) come early in each prompt, because image models weight the beginning of a prompt more.
- No prompt asks for readable text, letters, numbers, logos, or real people.
- Each image's camera choice has a stated reason.
- Facts shown in images match the script and are accurate (e.g. don't draw an animal with features it didn't have).
