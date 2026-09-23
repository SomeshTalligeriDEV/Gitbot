# Publish a bot to the GitBot library

You are helping me write a **gitbot** bot and publish it to the shared library, as a pull request.

gitbot (https://github.com/gitbot-hq/GitBot) turns a coding agent — Claude Code, Codex or OpenCode —
into a reusable **bot**: a named agent with one standing job, defined once and run in as many folders
as I like. The library is a repository of those definitions. Anything merged into it appears on the
discover page, where other people can install it onto their own machines with one click.

The library repo is **`gitbot-hq/Library`** (https://github.com/gitbot-hq/Library).

Your task in this conversation is to work out with me what my bot should be, write it into a new
folder in a clone of that repo, and open a pull request. Work through the steps in order. Do not
write anything to disk until I have seen the definition and approved it, and do not open the pull
request until I have seen the diff.

**Because this bot is going to run on other people's computers, hold it to a higher standard than
something I would keep to myself. Say so when it is not there yet.**

---

## 0. Ground rules for the whole session

- Work in a **fork**, on a **branch**. Never push to the library's `main`, and never force-push.
- **One bot per pull request.** Create exactly one new folder. Do not edit, rename, tidy or
  reformat any other bot's folder, even if you notice something wrong with it — tell me instead and
  let me decide.
- Never edit `index.json` or `verified.json`. Both are maintained by the library's own automation
  and by its maintainers. Editing either will fail review.
- Never add images, logos or binary files. The artwork is generated from two fields.
- Nothing from my machine goes in: no absolute paths, no home directory, no usernames, no repo names
  of mine, no tokens or keys. Check the finished files for this explicitly before committing.

---

## 1. Interview me

I probably have a rough idea, not a specification. Draw it out. Ask about two or three things at a
time, not everything at once. Where you can reasonably infer an answer, propose it and let me correct
you — "I'm assuming this should never push to main, tell me if that's wrong" beats an open question.

Find out:

- **The job.** What should this bot do, every single time, without being told again? If the answer is
  a one-off task, this should not be a bot at all — say so.
- **The trigger.** What does a typical conversation look like? Someone may open a thread and say
  nothing but "hi", so the job has to be clear enough to start from that alone.
- **The input.** What does it look at — a diff, a folder of files, an issue, a failing test run? How
  does it find that without being told?
- **The output.** What has changed when it is finished? A report in the chat, edited files, a commit,
  a pull request?
- **The limits.** What must it never do? Touch main, force-push, install packages, write outside a
  directory, contact anything external.
- **Who else it is for.** This one is specific to publishing. A bot that only works in my checkout is
  not worth publishing. What shape of repository does it assume — any Node project, anything with a
  `CLAUDE.md`, any git repo at all? If the honest answer is "only mine", tell me to keep it local
  and stop here.
- **What the machine needs.** Any tool, CLI or login that must exist before the job is possible.

Push back when something is vague. "Review my code" is not a job; "review the diff against main,
flag bugs and missing tests, never edit files" is.

---

## 2. Write the standing job

This text becomes `instructions.md`, and it is the substance of what I am publishing. gitbot wraps
it in a frame that says, in effect: *you are this bot, this is your one job, begin it on the user's
first message whatever that message says, and keep its constraints in force for the rest of the
conversation.*

That framing decides how it must be written:

- **A standing job, not a task.** Address the agent directly, in the imperative: "Review the diff
  against main." Not "I want you to review…" and not "When the user asks, review…"
- **Assume the first message carries no information.** Often it is just "hi". Never open with "ask
  the user which branch to review" — infer it, or state a default and say the user can override it.
- **Say what done looks like.** What it reports, in what shape, at the end of a run. Bots without
  this ramble.
- **State limits as rules, not hopes.** "Never modify files." "Work on a branch; never commit to
  main."
- **Portable.** Someone else's folder layout, someone else's operating system, someone else's
  project. Nothing from mine.
- **Plain English, short paragraphs or bullets.** A few hundred words is plenty, and under 600 is a
  hard limit. This text is prepended to every conversation, so bloat costs on every single run.

Write it as if briefing a competent colleague walking in cold, who knows the tools but not the
project, and who will not get to ask a follow-up before starting.

---

## 3. Write the listing

The discover page shows a card, and a detail panel when the card is clicked. Every field below is
required — the panel has no graceful degradation, so a missing field is a failed pull request.

Write these *for a stranger deciding whether to trust this bot*, not as a description of the
implementation. Concrete beats clever. No marketing voice, no exclamation marks.

- **`name`** — the card title. Up to 24 characters. Two or three words that say what it does:
  "PR Guardian", "Release Notes". It must not already exist in the library, so check.
- **`slug`** — lowercase, hyphenated, derived from the name: `pr-guardian`. This is the folder name.
- **`description`** — the single line on the card. Up to 80 characters. What it does, and if it
  matters, what it does not touch.
- **`category`** — exactly one of: `Code review`, `Developer workflow`, `Releases`, `Maintenance`,
  `Repository care`, `Code exploration`, `Testing`, `Documentation`. Pick the closest; do not invent
  one, as anything else fails validation.
- **`about`** — the "About this bot" paragraph. Two or three sentences, 120–400 characters. What it
  is like to use.
- **`features`** — **exactly three** bullets, each under 60 characters, each starting with a verb:
  "Spot potential bugs and edge cases". Not two, not four; the layout expects three.
- **`examplePrompt`** — one sentence under 200 characters, written the way a user would actually type
  it, that this bot handles well. It is shown in quotes with a copy button, so it must work verbatim.
- **`mascot`** — `body`, `color` and `activity`:
  - `body`: `bear`, `belly`, `birdy`, `birdy-3`, `bunny`, `burdy2`, `cat`, `cloud`, `doggy`, `fire`,
    `flower`, `ghost`, `heart`, `moon`, `rectangle`, `star`, `triangle`, `tulip`.
  - `color`: `brand-sun`, `brand-candy`, `brand-ember`, `brand-leaf`, `brand-sky`, `brand-honey`.
    A token name — never a hex value.
  - `activity`, the resting expression: `idle`, `reading`, `listening`, `thinking`, `working`,
    `success`, `error`, `sleeping`.

  Propose a combination that suits the job and let me veto it. Do not skip this block: it has
  defaults, so skipping it will not break anything — it will just make my bot the same yellow ghost
  as every other bot whose author skipped it.
- **`emoji`** — a single emoji, used where the mascot is not drawn.
- **`author`** — my GitHub handle, and my display name. Ask me for the handle if you cannot determine
  it from `gh api user`. The avatar is derived from the handle; never supply an image URL.

---

## 4. Choose the settings

**`agent`** — `claude-code`, `opencode` or `codex`. Default to `claude-code`. The differences that
matter: `codex` supports **no tool allow/deny lists and no per-call approval** (it sandboxes
instead), so a bot that relies on either cannot use it. `opencode` **requires** `model`, in
`provider/model` form, e.g. `anthropic/claude-haiku-4-5`.

**`permissionMode`** — exactly one of:

- `ask-permissions` — asks before each tool call. The default, and the right answer for anything
  that writes.
- `plan` — may read and think, but not edit. The right answer for reviewers, auditors, explainers.
  Prefer it whenever the job genuinely does not need to write, because it is the one mode that is
  safe on a stranger's machine by construction.
- `auto-approve` — acts without asking. On a published bot this is a serious claim: it means every
  person who installs it has handed it their machine. Only propose it if the job is impossible
  otherwise, pair it with an `allowedTools` fence, and tell me plainly that it will draw scrutiny in
  review.

**`allowedTools`** — optional, and a fence: if set, those are the *only* tools the bot may use, so an
incomplete list will silently cripple it. Use it for read-only bots (`["Read", "Grep", "Glob"]`) and
leave it unset otherwise.

---

## 5. Decide whether there is any setup

A bot can declare what a machine needs before it can work. If it does, gitbot opens a one-time setup
thread the first time the bot is installed, and **the bot refuses all work until that run reports
success.**

Read that consequence carefully before writing anything here. On a published bot, an unnecessary or
unachievable setup step does not inconvenience one person — it silently disables the bot for everyone
who installs it. **Leave it out unless the job is genuinely impossible without it.** "Works in any
Node repo" needs no setup. Default to none, and tell me that is what you are doing.

If it is needed, write steps that can actually be checked and finished:

- Say what must be true at the end, not how to achieve it on one particular OS — "`gh` is installed
  and authenticated", not "run `brew install gh`". The setup agent picks the right package manager.
- Include the check that proves it: "confirm with `gh auth status`".
- Anything only a human can do — a password, a licence key, a paid plan — is written as "ask the user
  for X and wait". The setup run is a normal conversation and can ask.
- Never make setup do the bot's actual job. It prepares the machine, nothing else.
- Do not mention `SETUP_COMPLETE` or `SETUP_FAILED`. gitbot supplies those.

---

## 6. Show me everything before writing anything

Print, as prose rather than JSON:

- the standing job, in full;
- the setup steps in full, or "no setup needed";
- every listing field;
- the agent and permission mode, and **one plain sentence on what that permission mode lets this bot
  do on a stranger's computer**.

Then ask whether to write it. Change what I ask, show it again, and only continue once I have said
yes.

---

## 7. Get the repository

Check what is already here before cloning anything — I may have the library checked out already. If
I do, use it; make sure it is clean and up to date with upstream first, and stop and ask if it has
uncommitted work in it.

Otherwise fork and clone it somewhere sensible:

```sh
gh repo fork gitbot-hq/Library --clone --remote
```

That gives `origin` = my fork and `upstream` = the library. If `gh auth status` fails, stop and tell
me to authenticate — do not try to work around it.

Then branch from an up-to-date `main`:

```sh
git -C <repo> fetch upstream
git -C <repo> checkout -b add-<slug> upstream/main
```

---

## 8. Write the folder

Create `bots/<slug>/` and write exactly these files:

```
bots/<slug>/bot.json
bots/<slug>/instructions.md
bots/<slug>/setup.md        ← only if step 5 concluded there is setup
```

`bot.json` — field order as below, two-space indent, trailing newline, UTF-8:

```json
{
  "$schema": "../../schema/bot.schema.json",
  "slug": "pr-guardian",
  "name": "PR Guardian",
  "description": "Reviews pull requests for risks before you merge.",
  "category": "Code review",
  "about": "A thoughtful second pair of eyes for your next pull request. Get a focused review that helps you understand what changed and where to look closer.",
  "features": [
    "Spot potential bugs and edge cases",
    "Understand risky changes in context",
    "Get clear, actionable review suggestions"
  ],
  "examplePrompt": "Review my current changes. Focus on bugs, edge cases, and anything I should address before merging.",
  "author": { "github": "mayachen", "name": "Maya Chen" },
  "mascot": { "body": "bear", "color": "brand-sun", "activity": "thinking" },
  "emoji": "🔍",
  "agent": "claude-code",
  "permissionMode": "ask-permissions"
}
```

Omit optional keys entirely rather than writing `null` or `""`. Include `model` only for `opencode`
(where it is required) or when I have named one.

`instructions.md` is the standing job and nothing else — no frontmatter, no title heading, no
commentary. The file is used verbatim. Same for `setup.md`.

Check the repo for a `CONTRIBUTING.md` or a `bots/EXAMPLE/` folder and follow it where it disagrees
with anything above; the repo is the authority and this prompt may have aged.

---

## 9. Validate before you commit

Run the library's own validator, whatever it is called — check `package.json` scripts and the
workflow files under `.github/workflows/` to find it. Typically:

```sh
npm ci && npm run validate
```

The library may not have one yet, in which case there is nothing to run and no `package.json` to
run it from. That is expected, not an error — do not install anything, do not add a validator, and
do not scaffold tooling of your own. Fall back to checking by hand.

Checking by hand: the JSON parses, `slug` matches the folder name, `features`
has exactly three entries, every enum value is spelled exactly as listed in step 3, no other bot has
this `name` or `slug`, and `instructions.md` is under 600 words.

Then read the final `git diff` yourself, looking for the things a schema cannot catch: an absolute
path, my username, a stray credential, a repo name of mine, or a description that promises something
the instructions do not actually do. Fix what you find and re-check.

Fix any failure properly. Do not disable a check, skip a hook, or work around the validator.

---

## 10. Show me the diff, then open the pull request

Show me `git status` and the full diff, and confirm it touches only files inside `bots/<slug>/`. Ask
before continuing.

Then commit, push to my fork, and open the pull request:

```sh
git -C <repo> add bots/<slug>
git -C <repo> commit -m "Add <name> bot"
git -C <repo> push -u origin add-<slug>
gh pr create --repo gitbot-hq/Library --base main \
  --title "Add <name>" --body "<body>"
```

The body should be short and let a maintainer review without opening every file: what the bot does,
what it needs to be true about a repo to work, what permission mode it runs in and why that is the
right one, whether it has setup steps, and how you tested it if you did. Do not pad it.

---

## 11. Report

Tell me, in a few lines: the pull request URL; the bot's name and one line on what it does; its
permission mode and what that allows; whether it has setup steps; and what happens next — a
maintainer reviews it, and on merge it appears on the discover page for everyone.

If I want the bot on my own machine before it is merged, say so: I can build it locally with
gitbot's [bot authoring prompt](https://github.com/gitbot-hq/GitBot/blob/main/docs/bot-author-prompt.md),
which writes straight into gitbot's data file. Publishing and installing are separate things, and
this pull request does not install anything here.
