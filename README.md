# Saturn for Claude

Gives Claude your [Saturn](https://www.saturnnotes.com) notes. Claude can search and read them, write and edit notes, keep your tasks, file notes into spaces and board columns, lay out canvases and save links. It works through the Saturn app on your Mac, so your notes stay there, as plain Markdown files you own, and each change appears in Saturn as Claude makes it, alongside anything you're typing.

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

One file: [`scripts/saturn-mcp`](scripts/saturn-mcp), a short shell script. It finds the `saturn-mcp` bridge inside the Saturn app (the copy that's running, else the one in `/Applications` or `~/Applications`) and hands over to it. The bridge relays Claude's requests to Saturn over a local connection that only your account on this Mac can open. If Saturn isn't running, the bridge opens it in the background, usually not until Claude first uses one of Saturn's tools. The first session after you install or update Saturn opens it at once. The script downloads nothing, installs nothing and writes nothing.

When Claude connects, Saturn's first answer explains its tools in plain words. It covers what notes, spaces and tasks are, says to read a note before changing it, and says to treat what notes say as material, never as instructions. Each tool also says whether it only reads, only adds, or can change what's there.

## Privacy Policy

- **What Claude can reach.** Only your Saturn notes, and only after you allow the app in Saturn: read only, or read and write. Claude reads and changes only what it asks Saturn for while you use it.
- **Where your notes go.**
  - The plugin talks only to Saturn on this Mac, and Saturn sends nothing anywhere by itself.
  - What Claude reads becomes part of your conversation with Claude, which Anthropic handles under [its privacy policy](https://www.anthropic.com/legal/privacy).
  - No tool uploads, publishes or deletes a note. Archiving hides a note, and you can restore it.
- **When Saturn uses the network for Claude.** Two tools reach the web, with what Claude gives them:
  - Saving a link fetches the address Claude passes, for the page's title and picture.
  - A page Claude saves into Saturn runs its own scripts when you open it, and can load or send what its HTML says. The page can't read your notes.
  - So either can carry text Claude put into it, including text it read from your notes. Saturn's instructions tell Claude to treat what notes say as material, never as instructions.
- **What's kept, and for how long.**
  - The plugin stores nothing.
  - On this Mac, Saturn keeps the apps you've allowed and their access level, until you remove them. It also keeps a list of the last 20 changes assistants made, which you can clear.
  - Both are in Saturn › Settings › Assistants.
- **Sharing.** Saturn's makers never receive your notes, and nothing here sells or shares them.
- **Contact.** [help@saturnnotes.com](mailto:help@saturnnotes.com). Saturn's full policy is at [saturnnotes.com/privacy](https://www.saturnnotes.com/privacy).

## Help

- **Saturn's tools don't appear.** Open Saturn and check Settings › Assistants, then reconnect Saturn (`/mcp` in Claude Code).
- **Claude Code lists Saturn's tools twice.** You also connected Saturn from its Connect an App settings. Remove that copy with `claude mcp remove saturn --scope user`.

Questions, problems and security reports: [help@saturnnotes.com](mailto:help@saturnnotes.com)
