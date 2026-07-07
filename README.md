# poormansadvisor

A Claude Code skill that implements Anthropic's [advisor strategy](https://claude.com/blog/the-advisor-strategy) using subagent routing instead of the API-only `advisor_20260301` tool.

## What it does

Pairs your current executor model with a more capable advisor model:

- **Sonnet/Haiku** agents consult **Fable**
- **Opus/Fable** agents consult **Codex**

The advisor provides analysis, recommendations, and concrete next steps without implementing anything. Your executor session gets expert guidance at a fraction of the cost of running the advisor end-to-end.

## Installation

Copy or symlink `SKILL.md` into your Claude Code skills directory:

```bash
# Option 1: symlink
ln -s /path/to/poormansadvisor ~/.claude/skills/poormansadvisor

# Option 2: copy
mkdir -p ~/.claude/skills/poormansadvisor
cp SKILL.md ~/.claude/skills/poormansadvisor/
```

## Usage

Manual invocation:
```
/poormansadvisor "should I restructure this schema?"
/poormansadvisor --fable "best approach for this refactor?"
/poormansadvisor --codex "is this migration safe?"
```

Auto-trigger: the skill is designed to fire automatically when an agent detects it's stuck, looping, or facing architectural uncertainty. See SKILL.md for trigger conditions.

## Auto-routing

When no `--fable` or `--codex` flag is given, the skill routes based on the current model — always consulting *up* to a more capable model.

## License

MIT
