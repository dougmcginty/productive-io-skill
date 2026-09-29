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

Do not commit credentials. Put them in a local environment file outside the installed skill folder, such as `~/.openclaw/.env`:

```env
PRODUCTIVE_API_TOKEN=your_token_here
PRODUCTIVE_ORGANIZATION_ID=your_org_id_here
PRODUCTIVE_PERSON_ID=your_person_id_here
```

Optional:

```env
PRODUCTIVE_API_BASE=https://api.productive.io/api/v2
```

The CLI auto-loads `~/.openclaw/.env` first and `~/.openclaw/workspace/.env` second. It also works with normal shell environment variables, which is useful if you prefer to launch Claude Code or Codex from a shell that already exports the Productive values.

### Codex install environment

1. Copy `variants/codex/productive/` into your Codex skills directory.
2. Create the env file if it does not exist:

   ```bash
   mkdir -p ~/.openclaw
   touch ~/.openclaw/.env
   chmod 600 ~/.openclaw/.env
   ```

3. Add the `PRODUCTIVE_*` variables shown above to `~/.openclaw/.env`.
4. From the installed skill folder, verify Codex can read the values:

   ```bash
   python3 scripts/productive_cli.py env-check
   ```

If you do not want to use `~/.openclaw/.env`, export the same variables in the shell or launcher environment used to start Codex.

### Claude Code install environment

1. Copy `variants/claude/productive/` into your Claude Code skills directory.
2. Store credentials outside the skill folder, preferably in `~/.openclaw/.env`:

   ```bash
   mkdir -p ~/.openclaw
   touch ~/.openclaw/.env
   chmod 600 ~/.openclaw/.env
   ```

3. Add the `PRODUCTIVE_*` variables shown above.
4. From the installed Claude skill folder, verify Claude Code can read the values:

   ```bash
   python3 scripts/productive_cli.py env-check
   ```

Claude Code also works when those variables are exported in the shell environment that launches it.

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
