---
name: mspaint-video-prompts
description: End-to-end workflow for faceless YouTube slideshow videos made of simple, flat, MS-Paint-style cartoon images (about one image every 3-8 seconds, with voiceover). Claude writes the narrator script (or uses the user's own), then, once the user shares voiceover timestamps, designs every image (camera angle, scene, character positions) and delivers complete copy-paste image prompts in a .txt file for Google Flow, Midjourney, DALL-E or similar tools. Use this skill whenever the user mentions faceless YouTube videos, slideshow-style videos, animated-looking photo videos, MS Paint or doodle style visuals, ElevenLabs voiceover plus images, scene-by-scene or timestamp-based image prompts, or wants a script and image prompts for any explainer, facts, story or history video, even if they don't name this style explicitly.
---

# MS-Paint-Style Slideshow Video: Script to Image Prompts

This skill turns a topic (or a ready script) into a full set of image prompts for a slideshow-style video. The look is a crude, flat, hand-drawn cartoon style with thick wobbly outlines and solid colors. Each image stays on screen for a few seconds while a voiceover plays.

Claude cannot generate images itself. The deliverable is prompts that the user pastes into an image tool (Google Flow, Midjourney, DALL-E, etc.). Don't claim specific features of those tools (reference images, saved styles, aspect-ratio menus) as verified; tell the user to check what their tool offers.

The user's pipeline: topic -> setup answers -> narration script -> user records voiceover (usually ElevenLabs) -> user gives timestamps -> Claude splits the narration into visual scenes, designs each image and writes its prompt -> user generates images -> user edits in CapCut/DaVinci/Canva.

Reply in the language the user writes in (Hindi, Hinglish, English, etc.). The image prompts themselves are always written in English, because image models follow English prompts most reliably.

## Step 1: Setup questions (required before any script)

On a new video workflow, three details must be known before a script is written or edited:

1. **Script source**: Claude writes the script from a topic / the user already has a script / the user has a rough idea and wants Claude to polish it
2. **Narration language**: Hindi / Hinglish (Roman script) / English / another language
3. **Video length**: about 2-3 min / about 5 min / about 8-10 min

The **topic** is also needed unless the user supplied their own finished script. It is free text, so it is never a multiple-choice option.

### Rules for collecting them

- **Skip only what the user has explicitly stated.** Read the user's message and the conversation so far. A detail counts as provided only if the user actually said it. Never guess, infer a default, or fill in a preference on the user's behalf.
- **A pasted script settles three things:** the script source, its narration language (the language the script is written in) and its length (the script's own length). Don't ask about those; ask only if something else is still missing.
- **A delegated choice is an answer.** If the user explicitly says "you choose" for an item, pick one, say what you picked in one line, and continue. Silence or a vague reply is not delegation.
- **Do not proceed without answers.** Do not write, outline or draft any part of the script until every required item is answered. Do not start the script "while waiting".
- **Ask each question once.** Once an item is answered, never ask it again. If the user answers only some items, ask only the remaining ones. If an answer is unclear, re-ask just that one item.

### How to ask

1. **Check the tools actually available in this conversation.** Use a native interactive question tool (a tappable poll, such as `ask_user_input_v0`) only if one is really present in the current tool list. Do not assume one exists, and do not attempt to call a tool that is not listed.
2. **If a native tool is available:** ask all the missing multiple-choice items in a single call. Put the topic question, if the topic is missing, in the short message written before the call. After the call, stop and wait for the answers.
3. **If no native tool is available:** send one plain-text message that lists only the unanswered items, each with lettered options, then stop and wait. For example:

   ```
   Before I write the script, I need a few details:

   1. Script source?
      a) Write it from my topic
      b) I already have a script
      c) I have a rough idea, polish it

   2. Narration language?
      a) Hindi  b) Hinglish (Roman script)  c) English  d) Other (tell me which)

   3. Video length?
      a) about 2-3 min  b) about 5 min  c) about 8-10 min

   And what is the topic?

   You can reply like "1a, 2c, 3b" plus the topic.
   ```

   Number and lay out only the items that are still unanswered, and drop the topic line if it is known or not needed.
4. Write the question and option text in the user's own language.

Once the answers arrive, confirm the plan in one or two lines and move to Step 2.

## Step 2: The narration script

Read `references/script-writing.md` before writing or editing a script.

- If the user supplied a script, preserve it exactly. Do not rewrite, reorder, trim or "improve" it. You may point out light fixes only (long sentences that will sound unnatural in a voiceover, unclear lines), and you change nothing unless the user says yes. If the user asks for edits, make only those edits.
- If Claude is writing it, keep facts accurate. If web search is available, verify specific claims (numbers, dates, names, "firsts") before putting them in the script. If a fact is uncertain or debated among experts, say so in the narration ("scientists think...") instead of stating it as settled.
- Keep the hook, body and payoff structure, the pacing, and the language rules from `references/script-writing.md`.

### Narration format

The narration is written as natural, continuous, voiceover-ready paragraphs, the way a person would actually speak it. It is not split into one idea per line, and no line is numbered. Don't force one sentence per line.

The copyable narration contains only the spoken words, and nothing else:

- no numbered lists, bullets, scene numbers or timestamps
- no section headings, labels (such as "Hook:" or "Outro:"), production notes or stage directions
- no markdown decorations (bold, italics, headings, dividers)
- natural punctuation and paragraph breaks only; paragraphs stay readable and flowing, and suit ElevenLabs

Show exactly one clean version of the narration, not a numbered copy plus an unnumbered copy. Put it in a single plain block that is easy to copy (a code block with nothing but the narration inside it). Anything else you want to say, such as the approximate word count or a note about uncertain facts, goes outside that block.

Don't plan scenes or images here. Scene splitting happens later, in Step 4.

### Handing over to the voiceover

After delivering the narration, tell the user the next step: generate the voiceover (for example in ElevenLabs) and send back the timestamps (see Step 3). Do not start planning images until they do.

## Step 3: Get the timestamps

The narration has no numbered lines, so timestamps are tied to the spoken text. Ask for them in this shape, but accept any reasonable format (for example, a time range plus the first words, or the full phrase being spoken):

```
0:00 - 0:04  Opening words of that stretch of narration
0:04 - 0:09  Opening words of the next stretch
```

If the user gives only start times, or only times plus a few words, match them against the delivered narration and say so if a match is unclear.

If the user only gives total audio length plus the script, estimate timing from word count, tell them clearly that it's an estimate, and that real timestamps will give a better match between image and voice. Never present estimated times as exact.

## Step 4: Segment the narration into scenes and plan the images

This is where the narration is first divided into visual scenes. Do it here, never in the narrator script.

- Split the narration at natural sentence or clause boundaries, using the timestamps. Do not change the narration's wording; each scene's text is an exact excerpt of the delivered narration.
- Aim for roughly one image per 5 seconds, but let the audio decide: a short stretch of 3-4 seconds can get its own image, and a long stretch (7-8 seconds or more) can be split into two images. Two very short stretches can share one image.
- Make a compact plan first: number, time range, the narration excerpt, and a one-line visual idea. Put this index at the top of the output file, and show only a brief summary in chat. Don't stop to ask for approval unless the user asked to approve the plan.
- Every image should show what the excerpt is *about*, so the viewer understands it even with the sound off.

## Step 5: Lock the style and the characters

Read `references/style-and-prompt-template.md`. Two things must be identical across all prompts so the images look like one video:

- **Master style block**: copy it verbatim into every prompt.
- **Character sheets**: for every recurring character or creature, write one fixed description (colors, shape, size, face, distinctive features) and paste it verbatim into every prompt where that character appears. Do not paraphrase it between prompts, since small wording changes produce visibly different characters.

## Step 6: Design each image

Read `references/camera-guide.md`. For every image, decide deliberately (not by default):

1. **Camera angle and shot size**, and *why* it suits this part of the narration (emotion, scale, detail, surprise)
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
LINE: "the exact narration excerpt for this image"
SHOT: low angle, medium shot. Why: makes the creature feel huge as the narration talks about its size.
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

Narration (before delivering the script):

- All required setup answers were given by the user (or explicitly delegated); none were invented.
- The narration is natural paragraphs, with no numbering, bullets, scene numbers, timestamps, headings, labels, notes or markdown inside it, and only one version is shown.
- A user-supplied script is unchanged unless the user asked for edits.

Image prompts (before delivering the file):

- Every part of the narration is covered by an image, with no gaps in the timeline, and each LINE is an exact excerpt of the delivered narration.
- Master style block and character sheets are verbatim in every prompt that needs them.
- Important things (style, subject, position, camera) come early in each prompt, because image models weight the beginning of a prompt more.
- No prompt asks for readable text, letters, numbers, logos, or real people.
- Each image's camera choice has a stated reason.
- Facts shown in images match the script and are accurate (e.g. don't draw an animal with features it didn't have).
