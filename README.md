# Saturn for Claude

Gives Claude your [Saturn](https://www.saturnnotes.com) notes. Claude can search and read them, write and edit notes, keep your tasks, file notes into spaces and board columns, lay out canvases and save links. It works through the Saturn app on your Mac, so your notes stay there, and each change appears in Saturn as Claude makes it, alongside anything you're typing.

## Requirements

- **Saturn for Mac** on macOS 15 or later, with Settings › Assistants › *Allow assistants to connect* turned on (the default).
- **Claude Code** (in a terminal, an IDE or the Code tab of the Claude desktop app), or **Cowork** through the Claude desktop app. Saturn's server runs on your Mac, so Claude on the web and on your phone can't reach it.
- Chats in the desktop app don't run plugin servers. To connect them, use Saturn › Settings › Connect an App › Claude.

## Install

In Claude Code:

```
/plugin install saturn --marketplace kylethacker/saturn-claude-plugin
```

In the Claude desktop app, for Cowork: Customize › Plugins › Add marketplace, enter `kylethacker/saturn-claude-plugin`, then install Saturn.

## Try asking

- "What did I decide about pricing? Check my notes."
- "Add 'Book the venue' to my tasks, due Friday."
- "Save a summary of this conversation as a note in my Research space."
- "Move my notes tagged #draft to the Review column."

## The first time

Saturn asks before Claude reads anything, naming the app that wants in: *"Claude Code" would like to access your notes in Saturn.* Choose **Allow**, **Allow Read Only** or **Don't Allow**. You can change or remove access at any time in Saturn › Settings › Assistants.

## What it runs

One file: [`scripts/saturn-mcp`](scripts/saturn-mcp), a short shell script. It finds the `saturn-mcp` bridge inside the Saturn app (the copy that's running, else the one in `/Applications` or `~/Applications`) and hands over to it. The bridge relays Claude's requests to Saturn over a local connection that only your account on this Mac can open, and it starts Saturn in the background if it isn't already running. The script downloads nothing, installs nothing and writes nothing.

## Privacy

The plugin connects only to Saturn on this Mac, and Saturn answers only the apps you've allowed. Nothing Claude can do through Saturn uploads, publishes or deletes a note: archiving hides a note, and you can restore it.

What Claude reads through Saturn becomes part of your conversation with Claude, under [Anthropic's privacy policy](https://www.anthropic.com/legal/privacy). Saturn's own policy is at [saturnnotes.com/privacy](https://www.saturnnotes.com/privacy).

## Troubleshooting

- **Saturn's tools don't appear.** Open Saturn and check Settings › Assistants, then reconnect Saturn (`/mcp` in Claude Code).
- **Claude Code lists Saturn's tools twice.** You also connected Saturn from its Connect an App settings. Remove that copy with `claude mcp remove saturn --scope user`.

Questions and security reports: [support@saturnnotes.com](mailto:support@saturnnotes.com)
