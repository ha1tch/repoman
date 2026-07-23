# repoman

Repository-discipline tooling in pure Python 3 (stdlib only). Built for
precise text editing, tracked-work registers, dormant-guard currency,
version sync, and interruptible release orchestration — in any
repository, driven by one optional `.repoman.json`.

## Requirements

- Python 3.10 or later. No third-party dependencies.

## Install

Copy `repoman/` into your repository (conventionally under `scripts/`
or as a sibling directory), or clone and call the tools by path. A
repository opts in with `.repoman.json` at its root — an empty `{}` is
valid; every key has a documented default (`repoman/config.py`).

Run `python3 selftest.py` after install. Eighteen checks; exit 0 is
the acceptance gate. Do not trust an installation whose selftest fails.

## Tools

| Tool | Purpose |
|------|---------|
| `ed.py` | Journaled handle-based editing: `find` / `apply` / `sub --expect` / bounded `undo` (`selftest` embedded) |
| `roles.py` | Syntactic-role auditor: classify every occurrence of a term before substituting |
| `register.py` | Work-register operations: `add` / `close` / `check` over a tracking document, closures recorded append-only |
| `guards.py` | Dormant-guard registry: `stale` / `handoff` / `record` for verification that does not run by default |
| `syncver.py` | Version sync: plain VERSION file plus regex-targeted stamps in code or docs |
| `relcore.py` | Manifest-driven release orchestration: durable journal, `--resume`, no-display-pipes logging, archive builtin with embedded SHA-256 manifest, contamination scan, and binary sniff |

Every tool supports `--help`; every refusal names what to do next; the
process exit code is the only success signal. Full command output goes
to per-run log files — the tools are designed so no caller ever needs
to pipe their output to read it, because piping is how exit codes get
silently disarmed.

The suite is suitable for constrained or interruptible environments —
CI runners with execution ceilings, containers that reap processes,
laptops that sleep mid-run. Interrupted work resumes from its journal;
nothing completed is lost.

## Configuration

See `repoman/config.py` for defaults and `repoman/relcore.py` for the
release-manifest schema, including a worked example.

## License

GPLv3.0 - Copyright (c) 2026 haitch. https://ual.li
