# Installing opc-superpowers for Codex

Enable opc-superpowers skills in Codex via native skill discovery. Just clone and symlink.

## Prerequisites

- Git

## Installation

1. **Clone the opc-superpowers repository:**
   ```bash
   git clone https://github.com/kaelzhang/opc-superpowers.git ~/.codex/opc-superpowers
   ```

2. **Create the skills symlink:**
   ```bash
   mkdir -p ~/.agents/skills
   ln -s ~/.codex/opc-superpowers/skills ~/.agents/skills/opc-superpowers
   ```

   **Windows (PowerShell):**
   ```powershell
   New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills"
   cmd /c mklink /J "$env:USERPROFILE\.agents\skills\opc-superpowers" "$env:USERPROFILE\.codex\opc-superpowers\skills"
   ```

3. **Restart Codex** (quit and relaunch the CLI) to discover the skills.

## Migrating from old bootstrap

If you installed opc-superpowers before native skill discovery, you need to:

1. **Update the repo:**
   ```bash
   cd ~/.codex/opc-superpowers && git pull
   ```

2. **Create the skills symlink** (step 2 above) — this is the new discovery mechanism.

3. **Clean up legacy paths** if you previously used the old `superpowers` name:
   ```bash
   rm -f ~/.agents/skills/superpowers
   rm -rf ~/.codex/superpowers
   ```

4. **Remove the old bootstrap block** from `~/.codex/AGENTS.md` — any block referencing `superpowers-codex bootstrap` or `opc-superpowers-codex bootstrap` is no longer needed.

5. **Restart Codex.**

## Verify

```bash
ls -la ~/.agents/skills/opc-superpowers
```

You should see a symlink (or junction on Windows) pointing to your opc-superpowers skills directory.

## Updating

```bash
cd ~/.codex/opc-superpowers && git pull
```

Skills update instantly through the symlink.

## Uninstalling

```bash
rm ~/.agents/skills/opc-superpowers
```

Optionally delete the clone: `rm -rf ~/.codex/opc-superpowers`.
