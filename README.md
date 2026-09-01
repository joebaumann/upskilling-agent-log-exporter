# agent-logs

Collects the session logs your coding agents already write on your own machine and puts copies of them in a single zip file.

**Nothing is uploaded.** The tool makes no network calls of any kind. It reads files that are already on your disk and writes a zip next to itself. You decide what goes in before anything is written, and you can look inside the zip before sending it.

## What you need

Python 3.9 or newer.

Check what you have:

```bash
python3 --version        # macOS / Linux
python --version         # Windows
```

## Running it

Open a terminal and run:

```bash
./agent-logs
```

If that says "permission denied", call Python directly instead:

```bash
python3 agent-logs        # macOS / Linux
python agent-logs         # Windows
```

By default it covers the last 31 days.

## What it will ask you

It walks you through three questions:

1. **Agents.** If it finds logs from a coding agent you did not ask for, it tells you how many sessions and prompts it found and asks whether to include them.
2. **Projects.** It lists every project folder you have used an agent in, with the number of sessions, the number of prompts and the size, then asks whether to export all of them. If not, you give the numbers of the ones to leave out — `3 7 12-15` or `3,7,12-15`.
3. **Sessions.** For each project you left out, it lists the individual sessions with their date, length, size, number of prompts and opening message, and asks whether to drop all of them or only some.

Anything you exclude is not included in the zip.

When it finishes you get a file like `agent-logs-20260821-143500.zip` in the folder you ran it from, and a summary of what went in.

## Useful options

You will probably not need any of these, but:

| Option | What it does |
| --- | --- |
| `--start-date 2026-01-01` | Start from a specific day instead of 31 days ago. |
| `--start-date 7d` | Just the last 7 days. `all` for everything. |
| `--end-date 2026-08-01` | Stop at a specific day. Default is today. |
| `--dry-run` | Show exactly what would be exported and write nothing. |
| `--agents claude codex` | Only these agents. |
| `-o somewhere/mine.zip` | Put the zip somewhere else. |
| `--help` | The full list. |


## What ends up in the zip

The zip contains the transcript files, plus a `README.txt` and counts of how many sessions and prompts came from each agent. Because they are complete transcripts, they contain what those sessions contained: the messages you typed, the model's replies, the commands the agent ran, file paths on your machine, and parts of files it read.

## If something goes wrong

- **"no agent logs found on this machine"** — none of the places coding agents keep their transcripts (`~/.claude`, `~/.codex`, `~/.cursor`, and the equivalents for other agents) exist here, so there is nothing to export.
- **"command not found: python3"** — try `python` instead, or install Python from [python.org](https://www.python.org/downloads/).
- **"permission denied: ./agent-logs"** — use `python3 agent-logs` as above.
- **Anything else** — send the error message, along with the output of `./agent-logs --dry-run`, to vishakhp@stanford.edu and joachimbaumann@stanford.edu.