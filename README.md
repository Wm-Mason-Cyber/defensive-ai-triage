# Defensive AI Triage — Local Lab

An AP Cybersecurity lab. You are a Tier-1 analyst in a Security Operations Center (SOC).
Thirteen alerts are waiting in your queue. For each one you'll read the raw logs, decide
whether it's a real attack or a false alarm, and then compare your judgment against a small
**AI model running locally** on your own machine (through Ollama — nothing leaves your computer).

Full instructions are in **[`STUDENT_LAB.md`](STUDENT_LAB.md)**. Start there.

## What's here

| Path | What it is |
| :---- | :---- |
| **`STUDENT_LAB.md`** | The lab handout — read this first. |
| **`cases/`** | 13 cases. Each folder has an `ALERT.txt` (the alert you're triaging) and one or more log files. |
| **`ai/Modelfile`** | Recipe that builds the `triage-analyst` AI model. |

## Quick start

```bash
# 1. Build the local triage model (one time)
ollama pull qwen3:4b-instruct
ollama create triage-analyst -f ai/Modelfile

# 2. Read a case yourself, THEN ask the AI
cat cases/case01/ALERT.txt
less cases/case01/auth.log
cat cases/case01/ALERT.txt cases/case01/auth.log | ollama run triage-analyst
```

See `STUDENT_LAB.md` for the vocabulary, the log-reading field guide, the triage worksheet,
and the experiments to run.

## Requirements

* [Ollama](https://ollama.com) installed and running.
* The `qwen3:4b-instruct` model (~2.5 GB download; runs in ~4 GB of GPU memory). On an older
  GPU or CPU-only laptop, edit the `FROM` line in `ai/Modelfile` to `llama3.2:3b` instead.
* A terminal with `cat`, `less`, `grep`, `awk` (any Linux/macOS/WSL shell).

> **Privacy note:** this model runs entirely on your machine. In the real world, pasting
> company logs into a public chatbot can leak usernames, IP addresses, and internal
> hostnames. Running a model locally is one way to use AI for defense *without* sending
> sensitive data to someone else.
