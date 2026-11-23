# Writing the narrator script

Use this when Claude writes the script, or when checking a script the user supplied.

## Contents
1. Length and pacing
2. Structure
3. Writing for a voiceover (ElevenLabs and similar)
4. Language notes (Hindi, Hinglish, English)
5. Accuracy
6. Output format (one clean, unnumbered version)

## 1. Length and pacing

Rough guide for words of narration:

| Video length | English words | Approx. images (at ~5 s each) |
|---|---|---|
| 2-3 min | 300-450 | 25-36 |
| 5 min | 650-750 | 55-65 |
| 8-10 min | 1,100-1,500 | 95-120 |

These are estimates. Speaking speed depends on the voice and settings, and Hindi usually runs at a different word count per minute than English. The real length is known only after the user generates the audio, so say that, and rely on their timestamps for the actual image timing.

## 2. Structure

- **Hook (first 5-10 seconds)**: a surprising fact, a question, or a bold claim about the topic. No "Hello friends, welcome to my channel" intro unless the user wants one.
- **Body**: a few clear sections, each building on the last. Order facts so curiosity keeps growing (a small surprise first, the biggest one later).
- **Payoff / ending**: a final fact, a twist, or a one-line takeaway. Add a call to action (subscribe, comment) only if the user asks for one.

## 3. Writing for a voiceover

- **Write natural, continuous paragraphs**, the way a person would actually say it out loud. Do not split the script into one idea per line, and do not number anything. Scene splitting happens later, in Step 4 of SKILL.md, from the user's timestamps, not in the script.
- Short, plain sentences, each easy to say in one breath. Avoid stacked clauses, brackets, and long lists inside one sentence.
- Write numbers the way they should be spoken ("sixty-six million years ago" in English narration), since voice tools can misread digits and abbreviations.
- Avoid hard-to-pronounce names without help. If a name is tricky (a long dinosaur name), tell the user and offer a phonetic spelling to paste into the voice tool.
- Use punctuation to control pauses: commas for a short pause, full stops for a longer one, an ellipsis for a dramatic beat. Use sparingly.
- Don't write stage directions, visual notes, labels ("Hook:", "Outro:"), numbers, bullets or markdown inside the narration text, because the user will paste it straight into the voice tool. Keep the script clean, and put anything else outside it.

## 4. Language notes

- **English**: simple, conversational, no jargon without a one-line explanation.
- **Hindi**: write in Devanagari by default, because voice tools generally pronounce Hindi better from Devanagari than from Roman letters. Suggest the user test a short sample first, and switch if the result sounds off.
- **Hinglish**: write in Roman script, which is what the setup question offers. Don't ask the script question again. Use a Devanagari/English mix only if the user explicitly asks for it, since voice tools handle mixed scripts differently. Keep English terms in English when they're the natural word (for example "fossil").
- Whatever the language, keep the tone of a friendly storyteller, not a textbook.
- Image prompts are always in English, whatever the narration language is.

## 5. Accuracy

- Verify specific facts (numbers, dates, sizes, "first/biggest/only" claims) with web search when it's available.
- When something is uncertain or debated, phrase it that way ("scientists believe...", "evidence suggests...").
- Don't invent statistics, quotes or sources to make a line sound stronger.
- If the user's own script contains something that looks wrong, point it out politely and let them decide.

## 6. Output format (one clean, unnumbered version)

Present the narration exactly once, as natural, voiceover-ready paragraphs inside a single plain code block, with nothing but the spoken words in it:

- no numbered lines, bullets, scene numbers or timestamps
- no headings, labels, production notes or stage directions
- no bold, italics, dividers or other markdown decoration
- natural punctuation and paragraph breaks only

Don't show a second, numbered copy. Anything else (approximate word count, a note about an uncertain fact, a phonetic spelling for a hard name) goes outside the code block.

If the user supplied the script, don't reprint it renumbered, split or reformatted; keep it exactly as given and put any suggested fixes outside it.

After the narration, tell the user to generate the voiceover and send back timestamps once the audio is ready. Timestamps are matched to the spoken text, so they don't need line numbers.
