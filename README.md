# Productive.io Skill

Explicit-only OpenClaw, Codex, and Claude skill variants plus a stdlib Python CLI for Productive.io timesheet work.

## Contents

- `variants/openclaw/productive/` - OpenClaw-oriented skill folder
- `variants/codex/productive/` - Codex skill folder
- `variants/claude/productive/` - Claude skill folder
- root `SKILL.md`, `agents/`, and `scripts/` - legacy OpenClaw/Codex layout kept for backward compatibility

Each variant includes:

- `SKILL.md` - skill instructions
- `scripts/productive_cli.py` - Productive.io helper CLI
- `agents/openai.yaml` where that platform uses it

## Configuration

Do not commit credentials. The cleanest setup is to export these variables in the shell or launcher environment that starts Codex or Claude Code. If you prefer a file, use a neutral local config file outside the installed skill folder:

```bash
mkdir -p ~/.config/productive-io-skill
touch ~/.config/productive-io-skill/.env
chmod 600 ~/.config/productive-io-skill/.env
```

Add:

```env
PRODUCTIVE_API_TOKEN=your_token_here
PRODUCTIVE_ORGANIZATION_ID=your_org_id_here
PRODUCTIVE_PERSON_ID=your_person_id_here
```

Optional:

```env
PRODUCTIVE_API_BASE=https://api.productive.io/api/v2
```

The CLI loads values in this order:

1. Already-exported environment variables from the running shell or launcher
2. `~/.config/productive-io-skill/.env`
3. `~/.productive-io-skill.env`
4. Legacy OpenClaw fallbacks: `~/.openclaw/.env`, then `~/.openclaw/workspace/.env`

The OpenClaw fallbacks exist only for backward compatibility. New Codex and Claude Code installs should prefer exported env vars or `~/.config/productive-io-skill/.env`.

### Codex install environment

1. Copy `variants/codex/productive/` into your Codex skills directory.
2. Either export the `PRODUCTIVE_*` variables in the environment used to launch Codex, or create the neutral env file:

   ```bash
   mkdir -p ~/.config/productive-io-skill
   touch ~/.config/productive-io-skill/.env
   chmod 600 ~/.config/productive-io-skill/.env
   ```

3. Add the `PRODUCTIVE_*` variables shown above to `~/.config/productive-io-skill/.env`.
4. From the installed skill folder, verify Codex can read the values:

   ```bash
   python3 scripts/productive_cli.py env-check
   ```

### Claude Code install environment

1. Copy `variants/claude/productive/` into your Claude Code skills directory.
2. Either export the `PRODUCTIVE_*` variables in the environment used to launch Claude Code, or create the neutral env file:

   ```bash
   mkdir -p ~/.config/productive-io-skill
   touch ~/.config/productive-io-skill/.env
   chmod 600 ~/.config/productive-io-skill/.env
   ```

3. Add the `PRODUCTIVE_*` variables shown above to `~/.config/productive-io-skill/.env`.
4. From the installed Claude skill folder, verify Claude Code can read the values:

   ```bash
   python3 scripts/productive_cli.py env-check
   ```

## Quick Check

```bash
python3 variants/codex/productive/scripts/productive_cli.py env-check
```

## Common Commands

```bash
python3 variants/codex/productive/scripts/productive_cli.py scheduled --from 2026-09-14 --to 2026-09-20
python3 variants/codex/productive/scripts/productive_cli.py projects --person-id 123456
python3 variants/codex/productive/scripts/productive_cli.py services --project-id 123456
python3 variants/codex/productive/scripts/productive_cli.py add-time --date 2026-09-14 --hours 1 --service-id 123456 --note "Work note"
```

The CLI uses Productive's JSON:API v2 endpoints and only Python standard library modules.

## Install Notes

- OpenClaw: copy `variants/openclaw/productive/` into the configured OpenClaw skills directory.
- Codex: copy `variants/codex/productive/` into the configured Codex skills directory.
- Claude: copy `variants/claude/productive/` into the configured Claude skills directory.
