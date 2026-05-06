# navi-cheatsheets

Personal [navi](https://github.com/denisidoro/navi) cheatsheets, ported from [sman-snippets](https://github.com/ickc/sman-snippets).

## Installation

```bash
# Add as a custom cheatsheet path
export NAVI_PATH="/path/to/navi-cheatsheets"

# Or symlink into navi's default location
ln -s /path/to/navi-cheatsheets ~/.local/share/navi/cheats/personal
```

## File Organization

Each `.cheat` file corresponds to an original sman `.yml` file:

| File | Topics |
|------|--------|
| `bash.cheat` | find, grep, rg, tar, du, ACLs, wget, ghostscript, IP tools, PDF, iperf, etc. |
| `btrfs.cheat` | btrfs filesystem management, scrub, balance |
| `git.cheat` | git operations: log, diff, clone, reset, merge, batch, worktree |
| `hpc.cheat` | HPC environment modules, SLURM, OpenSSL PKCS12 |
| `jekyll.cheat` | Jekyll serve |
| `linux.cheat` | Linux admin: mount, firewall-cmd, xrandr, mkfs, systemd |
| `mac.cheat` | macOS: Finder defaults, Spotlight, diskutil, metadata |
| `misc.cheat` | pandoc, ffmpeg, whisper, kitty, f3, gitit, cleanup |
| `package.cheat` | Package managers: suse, rhel, arch, apt, brew, port, nix, conda, pip, etc. |
| `programming.cheat` | Code cleanup, Jupyter, formatting (ruff, clang-format, rustfmt, shfmt, nixfmt) |
| `ssh.cheat` | SSH tunnels, rsync, sshfs, wake-on-LAN |
| `zfs.cheat` | ZFS pool/dataset management, snapshots, send/receive |

## Porting Decisions

### Variable translation

| sman syntax | navi equivalent |
|-------------|-----------------|
| `<<var>>` | `<var>` (free-text input) |
| `<<var(opt1,opt2)>>` | `<var>` + `$ var: echo -e "opt1\nopt2"` |
| `<<var( ,value)>>` | `<var>` + `$ var: echo -e " \nvalue"` (space = disabled) |
| `<<var#hint>>` | `<var>` + `; hint` comment above `$` line |

Variable names were converted to snake_case (navi requires alphanumeric + underscore).

### Snippet naming

Each command's `#` description line preserves the original colon-separated name for searchability:

```
# find:extension — show counts of all extensions...
```

### Snippet nesting

sman's `s r <snippet>` calls are translated to:

```bash
navi --query "<snippet-name>" --best-match
```

This invokes navi to find and execute the referenced snippet. When the original passed arguments to `s r`, the referenced command was inlined instead.

### Tag grouping

Related snippets are grouped under `%` tag headers using the pattern `% file_topic, sub_namespace` (e.g., `% bash, find`, `% git, reset`, `% package, arch`).

### Skipped content

The following were not ported:

- **Entire files**: `c3.yml`, `dautil.yml`, `polarbear.yml` (project-specific physics research), `install.yml` (outdated tool installers)
- **Machine-specific snippets**: references to specific institutional machines, IPs, or VPNs
- **Obsolete tools**: hub (replaced by gh), flake8/autopep8/isort (replaced by ruff), scipy weave, etc.

### Known limitations

- **"Empty" option UX**: sman allowed `<<flag( ,--delete)>>` where selecting the first (space) option meant "disabled". In navi, this is represented as `$ flag: echo -e " \n--delete"` — the space option appears blank in the fzf selector, which is less discoverable but functionally equivalent.
- **Cross-snippet calls**: `navi --query ... --best-match` is less robust than sman's direct `s r` invocation — fuzzy matching may pick the wrong snippet if descriptions are similar.
- **Multi-line commands**: Some complex multi-line sman commands were collapsed to single-line with `&&`/`;` separators for navi compatibility.
