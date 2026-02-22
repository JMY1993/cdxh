# cdxh

`cdxh` is a small launcher/helper for switching `CODEX_HOME` quickly, with alias management and shadow syncing.

## Features

- Run Codex with a selected home: `cdxh <alias_or_path>`
- Alias management:
  - `cdxh alias list|get|add|set|rm`
- Resolve target home path:
  - `cdxh show home <alias_or_path>`
- Shadow sync (non-auth data sharing):
  - `cdxh shadow <source_home> <target_alias> [flags]`

## Install

```bash
chmod +x ./cdxh
# optional: put it in PATH
ln -sf "$(pwd)/cdxh" ~/scripts/cdxh
```

## Usage

```bash
cdxh --help
cdxh alias add h0 ~/.codex --mkdir
cdxh h0
cdxh show home h0
```

## Shadow sync

```bash
cdxh shadow <source_home> <target_alias> [--path <dir>] [--auth-from <home>] [--force] [--copy]
```

Default behavior:

- Keep target auth as-is (no auth copy)
- Sync non-auth data from source
- Default sync mode is symlink (real-time sharing)
- Metadata is stored at `~/.config/cdxh/shadows.json`

### Flags

- `--path <dir>`: explicit target home path
- `--auth-from <home>`: explicitly copy auth from another home
- `--force`: replace managed target paths and re-apply metadata
- `--copy`: one-time copy mode instead of symlink

## Config files

- `~/.config/cdxh/aliases.json`: alias -> absolute path mapping
- `~/.config/cdxh/shadows.json`: shadow metadata (source, mode, managed paths, timestamps)

## Dependencies

Runtime dependencies:

- `bash`
- `python3`
- `codex` (only needed when running `cdxh <alias_or_path>`)

Optional:

- `gh` (for GitHub repo operations)
- `jq` is **not required** by this script

## License

MIT
