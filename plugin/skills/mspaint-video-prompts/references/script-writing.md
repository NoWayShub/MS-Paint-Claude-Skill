# Writing the narrator script

Use this when Claude writes the script, or when checking a script the user supplied.

## Contents
1. Length and pacing
2. Structure
3. Writing for a voiceover (ElevenLabs and similar)
4. Language notes (Hindi, Hinglish, English)
5. Accuracy
6. Output format

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

- **One idea per line**, and lines that are short enough to be spoken in about 3-8 seconds. Each line should be drawable as a single image.
- Short, plain sentences. Avoid stacked clauses, brackets, and long lists inside one sentence.
- Write numbers the way they should be spoken ("sixty-six million years ago" in English narration), since voice tools can misread digits and abbreviations.
- Avoid hard-to-pronounce names without help. If a name is tricky (a long dinosaur name), tell the user and offer a phonetic spelling to paste into the voice tool.
- Use punctuation to control pauses: commas for a short pause, full stops for a longer one, an ellipsis for a dramatic beat. Use sparingly.
- Don't write stage directions or visual notes inside the narration text, because the user will paste it straight into the voice tool. Keep the script clean, and put anything else outside it.

## 4. Language notes

- **English**: simple, conversational, no jargon without a one-line explanation.
- **Hindi**: write in Devanagari by default, because voice tools generally pronounce Hindi better from Devanagari than from Roman letters. Suggest the user test a short sample first, and switch if the result sounds off.
- **Hinglish**: ask whether the user wants Roman script or a Devanagari/English mix, since voice tools handle mixed scripts differently. Keep English terms in English when they're the natural word (for example "fossil").
- Whatever the language, keep the tone of a friendly storyteller, not a textbook.
- Image prompts are always in English, whatever the narration language is.

## 5. Accuracy

- Verify specific facts (numbers, dates, sizes, "first/biggest/only" claims) with web search when it's available.
- When something is uncertain or debated, phrase it that way ("scientists believe...", "evidence suggests...").
- Don't invent statistics, quotes or sources to make a line sound stronger.
- If the user's own script contains something that looks wrong, point it out politely and let them decide.

## 6. Output format

Present the script as numbered lines, so it's easy to refer to them later:

```
1. <line>
2. <line>
...
```

Then also give the same script as clean continuous text in a code block, ready to paste into the voice tool with no numbers. After it, tell the user to send back the timestamps once the audio is ready.
