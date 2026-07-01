# grill-me

A skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that relentlessly interviews you, one question at a time, until everything you know about a topic is out of your head and on the page.

I built it because context is the whole game with AI right now. Same models, same prompts, and the person who feeds the machine more of the real picture wins. The problem is that I think I'm "done" giving context when I've covered the angles *I* thought of, not all the angles that exist. I'm biased toward my own context, and I skip right past the assumptions that feel obvious to me.

grill-me fixes that. When I run it, it interviews me one question at a time, gives me its best guess at each answer so I can just confirm or correct, and keeps pushing until the well is dry. It saves every answer to disk as it goes, so nothing gets lost as the conversation runs long.

I use it two ways:

- **On myself**, when I'm working through a decision and want to make sure I've actually thought it all the way through.
- **On new clients during onboarding**, because that's when the good context comes out and it's exactly the moment it usually gets lost.

## What's in here

- [`grill-me/SKILL.md`](grill-me/SKILL.md) — the skill itself. This is the whole thing.

## How to use it

Drop the `grill-me/` folder into your Claude Code skills directory (`.claude/skills/` in a project, or `~/.claude/skills/` globally), then say **"grill me about X"**.

The version here is genericized. My private copy wires into my own note vaults, retrieval layer, and companion skills; the method is identical. Adapt the capture paths and the "make it searchable" step to your own setup.

## License

MIT. Take it, change it, make it yours.
