# Morning Journal skill

A portable Agent Skill for a guided 10–15 minute morning journal. It asks one
question at a time, adapts to how you are feeling, helps build a small plan, and
saves a polished 1–2 page Markdown entry.

Works with [Claude Code](https://code.claude.com/docs/en/skills) and
[Cursor](https://cursor.com/docs/skills). Invoke it with `/morning-journal`.

## What it does

- Lets you begin with free-writing or guided questions
- Adapts for low, positive, or mixed moods
- Moves from reflection to a concrete next action
- Includes an optional work or creative-writing prompt
- Saves every session as its own timestamped Markdown post
- Combines a day's posts later on request without changing the originals
- Offers a separate public version edited for readability and safer sharing
- Uses diagrams and links only when they add value

## Install

Choose one location. A personal install makes the skill available in every
project; a project install keeps it limited to one repository.

### Claude Code — personal

```bash
mkdir -p ~/.claude/skills/morning-journal
curl -fsSL https://raw.githubusercontent.com/dtobin02/morning-journal-skill/main/SKILL.md \
  -o ~/.claude/skills/morning-journal/SKILL.md
```

### Claude Code — one project

Run from the project root:

```bash
mkdir -p .claude/skills/morning-journal
curl -fsSL https://raw.githubusercontent.com/dtobin02/morning-journal-skill/main/SKILL.md \
  -o .claude/skills/morning-journal/SKILL.md
```

### Cursor — personal

```bash
mkdir -p ~/.cursor/skills/morning-journal
curl -fsSL https://raw.githubusercontent.com/dtobin02/morning-journal-skill/main/SKILL.md \
  -o ~/.cursor/skills/morning-journal/SKILL.md
```

### Cursor — one project

Run from the project root:

```bash
mkdir -p .cursor/skills/morning-journal
curl -fsSL https://raw.githubusercontent.com/dtobin02/morning-journal-skill/main/SKILL.md \
  -o .cursor/skills/morning-journal/SKILL.md
```

### One install for both Claude Code and Cursor

Cursor also discovers Claude-compatible skill locations. If both applications
run on the same computer, install the skill once at
`~/.claude/skills/morning-journal/` and both can use it.

### Install with Git instead

For easy updates, clone the repository directly into a personal skill location:

```bash
git clone https://github.com/dtobin02/morning-journal-skill.git \
  ~/.claude/skills/morning-journal
```

Update later with:

```bash
git -C ~/.claude/skills/morning-journal pull --ff-only
```

## First use

1. Start a new Cursor or Claude Code session if the `/morning-journal` command
   does not appear immediately.
2. Type `/morning-journal`.
3. On first use, choose where entries should be stored. The suggested location
   is `~/Documents/morning-journal`, but any writable folder works.
4. Choose whether to write freely or answer questions.
5. Say **finish** whenever you want the journal synthesized and saved.
6. Choose whether to create a separate public sharing draft.

Each completed session creates a separate file such as:

```text
2026-07-17_091530.md
2026-07-17_142405.md
```

To create a day-level synthesis later, invoke `/morning-journal` and ask:

```text
Combine today's journal posts.
```

The skill writes `2026-07-17_combined.md` while preserving every source post.

### Public sharing drafts

After saving a private session or combined post, the skill offers to create:

```text
2026-07-17_091530_public.md
2026-07-17_combined_public.md
```

The public draft improves context and narrative flow while removing or
generalizing unnecessary names, locations, health and relationship details,
confidential work, private communications, and identifying information. It never
changes the private source or publishes anything. Review the draft yourself before
sharing it.

The chosen journal directory is stored locally at:

```text
~/.config/morning-journal/config.md
```

No personal content or configuration is stored in this GitHub repository.

## Verify the installation

- Confirm the exact path ends in `morning-journal/SKILL.md`.
- In Claude Code, open `/skills` or type `/morning-journal`.
- In Cursor Agent chat, type `/morning-journal`.
- If it is missing, restart the session after creating a previously absent
  top-level skills directory.

## Uninstall

Remove the installed skill folder (choose the path you used):

```bash
rm -rf ~/.claude/skills/morning-journal
# or
rm -rf ~/.cursor/skills/morning-journal
```

The journal entries and `~/.config/morning-journal/config.md` remain untouched.

## Safely try a third-party skill

A useful low-risk first exercise is Anthropic's prose-only
[`doc-coauthoring`](https://github.com/anthropics/skills/tree/main/skills/doc-coauthoring)
skill. It provides a structured writing workflow and does not bundle scripts.

### 1. Review before installing

Open its `SKILL.md` and check:

- Does it contain shell commands, scripts, network calls, or package installs?
- Does frontmatter grant `allowed-tools` or request broad permissions?
- Does it write, delete, publish, email, or upload anything?
- Are referenced scripts and files present and understandable?
- Is the repository and license trustworthy?

Do not install a skill you cannot explain at a high level. A `SKILL.md` is an
instruction file: treat it like code because it can tell an agent to run tools.

### 2. Install at project scope first

Testing in a disposable directory limits where the skill appears:

```bash
mkdir -p ~/skill-sandbox/.cursor/skills/doc-coauthoring
curl -fsSL \
  https://raw.githubusercontent.com/anthropics/skills/main/skills/doc-coauthoring/SKILL.md \
  -o ~/skill-sandbox/.cursor/skills/doc-coauthoring/SKILL.md
cd ~/skill-sandbox
```

For Claude Code, replace `.cursor` with `.claude`.

### 3. Invoke and observe

Start Cursor or Claude Code in `~/skill-sandbox`, then type:

```text
/doc-coauthoring
```

Try: “Help me draft a one-page proposal for a reading group.” Notice what the
skill changes about the questions, structure, and output. Do not grant unexpected
permissions.

### 4. Remove it

After the experiment:

```bash
rm -rf ~/skill-sandbox
```

If you like the skill, reinstall it at personal scope. Review upstream changes
before updating it later.

## Privacy and safety

Journal entries remain local unless you separately commit, sync, or upload their
folder. This skill does not send messages, publish content, or install software.
It pauses the normal flow if the user indicates imminent danger or self-harm.

## License

MIT — see [LICENSE](LICENSE).
