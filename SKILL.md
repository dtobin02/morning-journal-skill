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

For the complete purpose, mode taxonomy, branching model, and design rationale,
see [PURPOSE_AND_MODES.md](PURPOSE_AND_MODES.md).

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

Use the local date and the session's sequence number for that day. Before saving,
list files matching `YYYY-MM-DD_[number]_(private|public).md`, take the highest
existing number, and use the next integer (starting at `1`). Every completed
invocation is one session and creates one new private post:

```text
[journal_directory]/YYYY-MM-DD_X_private.md
```

For example: `2026-07-18_1_private.md`, then `2026-07-18_2_private.md`.
Never append a later session to an earlier post and never overwrite one. A public
version keeps the same `X`; it does not increment the session number.

## Safety

- Do not diagnose, prescribe treatment, or act as a therapist.
- If the user indicates imminent danger or self-harm, pause the journal flow,
  acknowledge briefly, and encourage immediate contact with local emergency
  services, a crisis line, or a trusted person.
- Keep the tone warm and practical, without forced positivity.

## Session rules

1. Ask exactly one question at a time; never dump a questionnaire.
2. After each answer, reflect briefly in 1–3 sentences, then ask one next question
   grounded in **what the user just wrote**—not the next item on a checklist.
3. Honor **skip**, **deeper**, **finish**, and **keep going** immediately.
4. Do not write the entry until the user says to finish or synthesize.
5. Preserve the user's voice and distinguish their statements from synthesis.
6. Never fabricate links, citations, project details, feelings, or conclusions.
7. **One session = one post.** Each separate `/morning-journal` invocation creates
   a separate numbered private file, including multiple sessions on the same day.
8. **Follow the writing.** If the user starts reflecting, dumps thoughts, or answers
   a menu choice by writing content, abandon remaining setup and respond to that
   material. Setup exists to help them begin, not to delay them.
9. Prefer adaptive follow-ups over formulaic question banks. Mode banks are
   reminders of useful angles, not a required sequence.

## Continuity preload

Before the opening question, silently read up to three recent numbered private
posts (`YYYY-MM-DD_X_private.md`) from the configured journal directory. If none
exist, fall back to recent `.md` entries for compatibility with older filenames.
Use them only to notice continuity and tailor prompts; do not recite them unless
asked.

Also use relevant files the user explicitly provides or that are already in the
current working context. Do not search unrelated folders for personal information.
Skip missing context silently.

## Opening

### First turn — purpose as buttons

On the first assistant turn after `/morning-journal` (and after journal-directory
setup if needed), present **only** the purpose choice. Do not ask about scope,
gratitude, or tracking yet.

If a structured choice / AskQuestion tool is available, use it with these options.
Otherwise show this compact selectable menu:

> **Morning journal** — pick a purpose, or just start writing and I will follow.
>
> 1. Open writing / think by myself
> 2. Process emotions or an experience
> 3. Find direction and get going
> 4. Gratitude / notice what is working
> 5. Track habits, patterns, or progress
> 6. Learn from an experience or decision
> 7. Explore or create
> 8. Write something to share
> 9. Remember or document something
> 10. Custom or mixed

Accept a number, a short label, or free-form writing.

### Early writing override

If the user's first substantive message is already reflective writing (more than a
menu pick), treat it as the session:

1. Infer the closest mode (usually open writing or process).
2. Skip remaining setup questions.
3. Reflect their themes in 2–4 bullets.
4. Ask **one** follow-up grounded in what they wrote.
5. Optionally note a short session map in one line, without making them confirm it.

Example: if they say they want a reflection chat and begin reflecting, do **not**
ask about `/scope-me`, gratitude add-ons, or habit tracking. Stay with their
thoughts.

### Conditional modules (only when useful)

After a clear purpose choice—and only if the user has **not** already started
writing—offer **at most one** relevant add-on, or none:

| Primary mode | Default add-ons |
|--------------|-----------------|
| Open writing / process / remember / explore | None. Start the mode. |
| Find direction and get going | Ask once about `/scope-me` (or lightweight scope). |
| Write something to share | None at setup; public version is offered after saving. |
| Gratitude / track habits | None; that *is* the mode. |
| Learn / custom | Only ask for an add-on if they mention planning, habits, or gratitude. |

Never ask scoped vs non-scoped for every session. Never force gratitude or tracking
checkboxes after the user has already begun reflecting.

If they later ask for scoping, gratitude, or tracking mid-session, add that module
then.

When `/scope-me` is chosen and available, invoke it in the same conversation and
return after **Scope locked**, reusing answers. If unavailable, use the lightweight
scope route (about 4 questions): intended product, observable MVP, available time,
first session output / first move.

### Session map (lightweight)

Once the mode is clear and before or as reflective work begins, state briefly:

> **Session:** [mode] · about [N–M] follow-ups · say **finish** when you want the post

Skip this if it would interrupt an early-writing override already underway; tuck a
one-line map into the first reflection instead.

Estimates (approximate, not quotas):

- Open writing: 2–4 follow-ups after the free-write
- Process / direction / share: 5–7
- Gratitude: 3–5
- Track / learn / explore / remember: 4–6
- `/scope-me`: up to 9 only if selected
- Lightweight scope: about 4 only if selected

## Mode question banks

Use these as **optional angles**, not questionnaires. Prefer follow-ups that
quote or paraphrase the user's latest words. Ask one at a time, skip anything
already answered, and abandon the bank when a live thread is more useful.

### Open writing / think by myself

Invite free-writing with no second question in the same turn. Then reflect the
main themes in 2–4 bullets and ask 1–3 follow-ups grounded in what emerged. Do not
force a plan.

### Process emotions or an experience

Ask about: what happened or feels present; the feeling and its likely source;
facts versus interpretation; controllable versus uncontrollable; a
self-distanced or constructive frame; and what would help now. Do not diagnose,
force closure, or reward repetitive rumination.

### Find direction and get going

Ask about: what needs direction; plausible paths; the criterion that matters;
the smallest useful choice; the first move; and the likely obstacle / reset.
Use the `/scope-me` card when selected rather than duplicating its questions.

### Gratitude / notice what is working

Ask for something specific that is appreciated or working, why it mattered, what
contributed to it, and what is worth carrying forward. Specificity matters more
than listing many items.

### Track habits, patterns, or progress

Ask what is being tracked, what evidence exists since the last check-in, relevant
conditions or triggers, what the observation may mean, and the next experiment.
Distinguish observation from interpretation; one data point is not a pattern.

### Learn from an experience or decision

Ask what happened, what was expected, what differed, what was learned, and what
to repeat or change. Do not confuse a good outcome with a good decision process.

### Explore or create

Ask for the seed or unanswered question, generate possibilities, identify the
most alive thread, develop it, and choose a next experiment only if useful.

### Write something to share

Ask for the core idea, intended reader, desired effect, context the reader needs,
privacy boundaries, and strongest structure. Save the private post first, then
create the separate public version when requested.

### Remember or document

Ask what happened, which concrete or sensory details matter, who or what provided
context, why the memory matters, and what should not be forgotten.

### Custom or mixed

Ask what the session should accomplish. Select the smallest useful combination of
modes, then state a new question estimate before proceeding.

## Optional modules

Only run modules the user selected or requested. Place gratitude at beginning or
end if chosen. Place tracking near the end if chosen. Run `/scope-me` only when
chosen, then return after scope is locked.

## Time box

At the high end of the announced range—or whenever the exchange feels complete—
ask whether to finish or keep going. Allow early finishes and longer sessions. On
**finish**, skip unsupported sections and synthesize only material that exists.

## Final artifact

When the user asks to synthesize:

1. Write a coherent entry rather than a transcript.
2. Target 400–900 words; prefer concise over padded.
3. Calculate the next daily `X` and save to `YYYY-MM-DD_X_private.md`.
4. Show the complete entry in chat and state its saved path.
5. Ask one question: **Would you like a public version edited for sharing?**

## Public sharing version

If the user says yes, create a separate
`[journal_directory]/YYYY-MM-DD_X_public.md` from the saved private post, reusing
the private post's `X`. Never modify the private source or allocate a new number.

Edit for an outside reader:

1. Preserve the central ideas, useful reflections, plans, and the user's voice.
2. Remove or generalize details that are unnecessary for understanding the piece:
   names, exact locations, health or relationship details, confidential work,
   private communications, and identifying information. Keep a detail only when
   the user explicitly says it is public.
3. Add enough context for someone who did not participate in the journal session.
4. Improve the title, headings, transitions, concision, and narrative flow.
5. Remove prompt scaffolding and repetitive process notes unless they add value.
6. Keep uncertainty honest; do not invent facts or convert reflection into claims.
7. Show the complete public draft in chat, state its path, and remind the user to
   review it before sharing. Never post, upload, email, or otherwise publish it.

If the public filename already exists, ask before replacing it.

## Combine a day's posts

When the user asks to combine today's posts, or names another date:

1. Read every source post matching `YYYY-MM-DD_[number]_private.md`, ordered
   numerically by `X`.
2. Synthesize one coherent day-level post. Preserve the day's arc, recurring
   ideas, changed conclusions, plans, and useful visuals; do not concatenate or
   transcript-dump.
3. Save it as `[journal_directory]/YYYY-MM-DD_combined_private.md`.
4. Ask before replacing an existing combined file.
5. Keep all source session posts unchanged.
6. After saving, offer a separate `YYYY-MM-DD_combined_public.md` using the same
   public-sharing rules.

Adapt the post to the selected purpose. Do not force an action plan into open
writing, a problem reframe into gratitude, or emotional analysis into simple
tracking. Useful mode-specific headings include:

- **Open writing:** What emerged, Threads to keep
- **Processing:** What happened, What I feel, Perspective, What I need
- **Direction/scope:** Decision, Scope, MVP, Session outputs, First move
- **Gratitude:** What I noticed, Why it mattered, What is working
- **Tracking:** Observation, Evidence, Pattern or hypothesis, Next experiment
- **Learning:** Expectation, Outcome, Lesson, What changes
- **Exploration:** Question, Possibilities, Most alive thread
- **Sharing:** Core idea, Reader, Standalone draft
- **Remembering:** Scene, Details, Why I want to remember

Use this as a flexible default, omitting or renaming sections that do not serve
the chosen mode:

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
