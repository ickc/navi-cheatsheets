# navi-cheatsheets

Personal [navi](https://github.com/denisidoro/navi) cheatsheets.

## Installation

```bash
# Add as a custom cheatsheet path
export NAVI_PATH="/path/to/navi-cheatsheets"

# Or symlink into navi's default location
ln -s /path/to/navi-cheatsheets ~/.local/share/navi/cheats/personal
```

## Layout

Each file groups snippets by tool or theme. Snippet names follow
`tool:area:verb` (e.g. `git:branch:delete`, `mac:spotlight:disable`,
`brew:install`).

| File | Topics |
|------|--------|
| `acl.cheat` | recursive chgrp/chmod, setgid+sticky workflows |
| `archive.cheat` | tar/unzip plus streaming http extract |
| `bash.cheat` | path/PATH inspection, dir summaries, tee redirects, batch convert |
| `btrfs.cheat` | btrfs device/filesystem/subvolume + scrub + balance |
| `disk.cheat` | du/df, locate db, md5sum, dd benchmarks, badblocks/SMART/hdparm, f3 |
| `git.cheat` | git operations across log/diff/clone/remote/submodule/reset/merge/branch/tag/cherry-pick/batch/push/commit/pull/worktree |
| `hpc.cheat` | Cray PrgEnv modules, Slurm squeue/sbatch, OpenSSL pkcs12 split |
| `jekyll.cheat` | jekyll serve |
| `jj.cheat` | jj parallel to git.cheat (see "Modern alternatives" below) |
| `junkyard.cheat` | snippets queued for deletion; review and prune |
| `kitty.cheat` | kitty terminal theme switcher |
| `linux.cheat` | mount, users, power, network, display, kernel, mkfs, udev, vm, firewall, mce |
| `mac.cheat` | kext, power, finder, metadata, defaults/launchservices, spotlight, apps, disk, system |
| `media.cheat` | ffmpeg, mediainfo, whisper, imagemagick, yt-dlp |
| `network.cheat` | local/public IP, http server, wget mirror, samba mount, iperf |
| `obsidian.cheat` | Obsidian config diff/sort |
| `package.cheat` | suse/rhel/rpm/arch/apt/mas/nix/devbox/port/brew/pip/conda/pixi/jupyter/go/vscode |
| `pdf.cheat` | Ghostscript merge/extract, pdfimages, pdftoppm |
| `programming.cheat` | cleanup, jupyter, python random/format, format:*, pandoc, html minify, sys |
| `ssh.cheat` | tunnels, rsync, sshfs, sshuttle vpn, wake-on-LAN |
| `zfs.cheat` | zpool/arc/dataset/snapshot management |
| `file-search.cheat` ↔ `file-search-modern.cheat` | find / fd (see below) |
| `text-search.cheat` ↔ `text-search-modern.cheat` | grep / rg (see below) |
| `text-edit.cheat` ↔ `text-edit-modern.cheat` | sed / sd (see below) |

## Modern alternatives

For find/grep/sed, the classic and modern versions live in parallel files
with the same section structure, same sequence, and same descriptions.
Snippet names use the tool as prefix so navi shows both side by side in
fzf:

| Classic | Modern | Parallel files |
|---------|--------|----------------|
| `find` | `fd` | `file-search.cheat` ↔ `file-search-modern.cheat` |
| `grep` | `rg` | `text-search.cheat` ↔ `text-search-modern.cheat` |
| `sed` | `sd` | `text-edit.cheat` ↔ `text-edit-modern.cheat` |
| `git` | `jj` | `git.cheat` ↔ `jj.cheat` |

The `git`/`jj` pair follows the same naming and relative ordering where
there is a clean jj equivalent. Git-only operations (e.g. `git submodule`,
`git tag`) are omitted from `jj.cheat` rather than carrying half-working
translations.

## Junkyard

`junkyard.cheat` holds snippets that didn't survive the refactor:
personal paths (`~/git/source/envoy`), defunct tools (gitit, EOL
Anaconda modules), hardcoded user/MAC/IP defaults that can't be
generalized, and duplicates. Review and `rm` whatever you agree should
go.

## Conventions

- Snippet names: `tool:area:verb`, snake_case variables.
- Section tags: `% <file>, <subarea>` (e.g. `% git, log`, `% mac, spotlight`).
- Variable choices follow navi's `$ name: echo -e "..."` form. Leading
  space (`echo -e " \nfoo"`) represents the "disabled" option, mirroring
  the original sman `<<flag( ,foo)>>` UX.
- Cross-snippet calls use `navi --query "name" --best-match`.
