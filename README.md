# dotclaude

My personal Claude Code configuration — kept here so I don't lose it across machines and reinstalls.

This is primarily for my own use. You're welcome to copy anything that looks useful, but it isn't meant as a polished, supported config for general consumption.

## Contents

- [CLAUDE.md](CLAUDE.md) — global instructions Claude Code loads for every project (coding style, TypeScript conventions, naming, formatting).
- [commands/](commands/) — custom slash commands:
  - [articlemd-to-social.md](commands/articlemd-to-social.md) — turn an article into social posts.
  - [repo-to-articlemd.md](commands/repo-to-articlemd.md) — turn a repo into an article draft.

## Usage

Clone or symlink the relevant pieces into `~/.claude/`:

```sh
git clone https://github.com/<you>/dotclaude.git ~/webwork/dotclaude
ln -s ~/webwork/dotclaude/CLAUDE.md      ~/.claude/CLAUDE.md
ln -s ~/webwork/dotclaude/commands       ~/.claude/commands
```
