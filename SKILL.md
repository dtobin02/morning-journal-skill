---
name: morning-journal
description: >-
  Run a 10–15 minute guided morning journaling session and synthesize a dated
  1–2 page Markdown journal post with key ideas, diagrams, and verified links.
  Use when the user says /morning-journal or asks for a guided morning journal.
disable-model-invocation: true
---

# /morning-journal — Morning journaling session

Run a reflective conversation, one question at a time, then save a polished dated
journal post. Default session length is 10–15 minutes, but follow the user's pace.

## First-run setup

Use `$HOME/.config/morning-journal/config.md` as the configuration file.

If it does not exist:

1. Ask one question: where should journal entries be saved?
2. Recommend `~/Documents/morning-journal` while accepting any path.
3. After confirmation, create the directory and config file:

```markdown
journal_directory: ~/Documents/morning-journal
```

Do not write either location before the user confirms. Expand `~` to the user's
home directory when reading or writing. If configuration cannot be saved, continue
chat-only and explain that no journal file was written.

If the config exists, read `journal_directory`. If it is missing or invalid, ask
the setup question again rather than guessing.

Use the local calendar date for `YYYY-MM-DD`. Save entries as
`[journal_directory]/YYYY-MM-DD.md`. If today's file already exists, append a
second entry after a horizontal rule under `## Later — HH:MM`; never overwrite it.

## Safety

- Do not diagnose, prescribe treatment, or act as a therapist.
- If the user indicates imminent danger or self-harm, pause the journal flow,
  acknowledge briefly, and encourage immediate contact with local emergency
  services, a crisis line, or a trusted person.
- Keep the tone warm and practical, without forced positivity.

## Session rules

1. Ask exactly one question at a time; never dump a questionnaire.
2. After each answer, reflect briefly in 1–3 sentences, then ask one next question.
3. Honor **skip**, **deeper**, **finish**, and **keep going** immediately.
4. Do not write the entry until the user says to finish or synthesize.
5. Preserve the user's voice and distinguish their statements from synthesis.
6. Never fabricate links, citations, project details, feelings, or conclusions.

## Continuity preload

Before the opening question, silently read up to three recent `.md` entries from
the configured journal directory. Use them only to notice continuity and tailor
prompts; do not recite them unless asked.

Also use relevant files the user explicitly provides or that are already in the
current working context. Do not search unrelated folders for personal information.
Skip missing context silently.

## Opening

Start with:

> **Morning journal** — about 10–15 minutes, one question at a time. We'll end
> with a 1–2 page dated journal post.
>
> Do you want to **start by writing your thoughts**, or **be asked questions**?

For **writing**, invite free-writing without adding another question. When the
user finishes, reflect the main themes in 2–4 bullets and ask one useful follow-up.

For **questions**, proceed to Arrive.

## Adaptive flow

### 1. Arrive

Ask, one at a time and with natural wording:

1. How are you feeling right now—mood, energy, body, or whatever fits?
2. What feels most present this morning: a problem, hope, project, or noise?

### 2. Understand

Choose the branch that matches what the user said.

**If they feel poorly, stuck, or heavy:**

1. Why do you think you are feeling this way?
2. Help separate facts from interpretation and controllable from uncontrollable.
3. Offer one constructive problem frame and ask the user to correct it.
4. Ask what “a little better by tonight” would look like.

**If they feel good, steady, or energized:**

1. What do you think is working?
2. What conditions or habits are supporting it?
3. What is worth protecting or amplifying today?

**If mixed or unclear:** ask one clarifying question, then choose the closer branch.

### 3. Build

Turn the central issue or opportunity into a small plan. Ask one at a time:

1. What outcome matters today—or this week if today is too narrow?
2. What single next action can take less than 30 minutes?
3. What obstacle is most likely?
4. If it appears, what response will you use?

### 4. Create

Offer one tailored prompt connected to a current work or creative project. Prefer
a project the user named or that appears in supplied context. Examples:

- “What is the sharpest unanswered question in this project?”
- “What would this paper, chapter, or scene need to earn one sentence of trust?”
- “What would you try if you were not allowed to polish?”

Capture the response, then ask whether to synthesize now or explore one thread
a layer deeper.

## Time box

After roughly 6–8 substantive exchanges, ask:

> Want to **finish and write the journal**, or **keep going**?

Allow early finishes and longer sessions. On **finish**, skip any unsupported
sections and synthesize only from material that exists.

## Final artifact

When the user asks to synthesize:

1. Write a coherent entry rather than a transcript.
2. Target 400–900 words; prefer concise over padded.
3. Save it to the configured dated path.
4. Show the complete entry in chat and state its saved path.

Use this structure, omitting sections that have no meaningful content:

~~~markdown
# [Descriptive title drawn from the central idea]

*[Weekday], [Month] [D], [YYYY]* · morning journal

## Snapshot
[Feeling and what was most present, using the user's language where possible.]

## Key ideas
- [Idea 1]
- [Idea 2]
- [Idea 3 only if earned]

## Reframe
[Constructive problem frame, or what is working and worth protecting. Keep
uncertainty honest.]

## Build plan
- **Outcome:** …
- **Next action:** …
- **Obstacle → response:** …

[Optional Mermaid diagram only when it clarifies a relationship, fork, or plan.]

## Create
**Prompt:** …

[The user's response, lightly edited only for clarity.]

## Carry into the day
[One sentence.]

## Links
- [Only verified links surfaced in the session; omit this section when none exist.]
~~~

Use Mermaid or compact checklists only when they materially clarify the ideas.
Do not add decorative images or force a visual every day.
