<div align="center">

# gitbot Library

**Ready-made bots for [gitbot](https://github.com/gitbot-hq/GitBot). Import one, point it at a folder, put it to work.**

[![npm version](https://img.shields.io/npm/v/@gitbot-hq/gitbot?label=%40gitbot-hq%2Fgitbot)](https://www.npmjs.com/package/@gitbot-hq/gitbot)

[Get gitbot](#get-gitbot) · [What is a bot?](#what-is-a-bot) · [Using a bot from the library](#using-a-bot-from-the-library) · [Suggest a bot](#suggest-a-bot)

</div>

> [!NOTE]
> **The first bots are coming soon.** This repository is where they will live. Watch or star the repo to hear when they land.

## What is this?

[gitbot](https://github.com/gitbot-hq/GitBot) lets you turn an AI coding agent — Claude Code, Codex or OpenCode — into reusable **bots** that run on your own machine. This library is the home for bots built with it: bots you can import instead of writing from scratch, and read to learn how a good bot is put together.

## Get gitbot

You need gitbot to use anything here.

```bash
npm install -g @gitbot-hq/gitbot
gitbot start
```

- **npm package:** [`@gitbot-hq/gitbot`](https://www.npmjs.com/package/@gitbot-hq/gitbot)
- **Source, docs and issues:** [github.com/gitbot-hq/GitBot](https://github.com/gitbot-hq/GitBot)

gitbot needs Node.js 18+ and at least one agent installed and logged in. The [gitbot README](https://github.com/gitbot-hq/GitBot#install) covers setup.

## What is a bot?

A bot is an agent you define once and reuse:

- **Instructions** — its standing job, e.g. *"Review the diff against main. Flag bugs and missing tests. Never modify files."*
- **An agent** — Claude Code, Codex or OpenCode — and optionally a model.
- **A permission mode** — ask before each tool, auto-approve, or plan only.
- **Tool lists** — optionally, the only tools it may use.
- **Setup steps** — optionally, what it needs on a machine (*"ffmpeg must be on PATH"*), which it checks or prepares once.

gitbot packs all of that into a **share code** — a single line starting with `gitbot:v1:` — that recreates the bot on another machine.

## Using a bot from the library

Once bots are published here, using one takes three steps:

1. Copy the bot's share code.
2. In the gitbot hub, click **Import a bot** and paste it.
3. Open a thread in the folder you want it to work in, and say hi.

Each bot will be published with its **instructions and setup steps in plain text** next to its share code, so you can read exactly what it does before you import it.

> [!WARNING]
> **Read a bot before you import it.** A share code is a set of instructions for an AI agent that runs on your machine with your file access. gitbot's import dialog shows only the bot's name and description, and a bot that has setup steps starts its setup run as soon as it is imported, in the permission mode the code carries. Only import codes you have read or whose author you trust — the same care you would give a script from the internet. See [gitbot's security notes](https://github.com/gitbot-hq/GitBot#security).

## Suggest a bot

Have a bot that earns its keep, or an idea for one? [Open an issue](https://github.com/gitbot-hq/Library/issues) and tell us what it does. Contribution guidelines will be added here together with the first bots.

## Links

- gitbot on npm — [npmjs.com/package/@gitbot-hq/gitbot](https://www.npmjs.com/package/@gitbot-hq/gitbot)
- gitbot on GitHub — [github.com/gitbot-hq/GitBot](https://github.com/gitbot-hq/GitBot)
- Report a problem with gitbot itself — [GitBot issues](https://github.com/gitbot-hq/GitBot/issues)
