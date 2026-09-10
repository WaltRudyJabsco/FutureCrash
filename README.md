# FUTURE CRASH // ZERO {"{"}VERSION{"}"} — Release Candidate

**A local AI workstation disguised as a slightly haunted 1980s terminal.**

Future Crash is a dependency-light terminal companion built around one local
Ollama model. It combines an ambient retro-computer dashboard with a Quick
Oracle, a conversational Workstation, persistent memory, hosted web search,
permissioned host-computer tools, recurring Threads, a model-controlled Signal
Field, system telemetry, glitches, fortunes, observations, and synthesized
bleeps.

The terminal is the idle state. The assistant is the machine underneath it.

## Future Crash + LOOK

**Future Crash works by itself, but it was designed to live alongside LOOK.**

Future Crash is the ambient AI surface; LOOK is the fast, quiet inspection layer underneath it. Press `esc` from Future Crash to drop directly into your real interactive shell, use `lk` to inspect files, processes, ports, Git, Ollama, networking, and the machine itself, then type `exit` or press `ctrl-d` to return to Future Crash exactly where you left it.

```text
FUTURE CRASH
     │ esc
     ▼
real shell  →  lk machine
            →  lk ports
            →  lk git .
            →  lk ollama status
     │ exit / ctrl-d
     ▼
FUTURE CRASH
```

The projects remain deliberately independent. LOOK is not bundled with Future Crash and neither requires the other. They work together because they share the shell.

**Recommended setup: install both.**

> **LOOK repository:** replace this line with the current LOOK GitHub URL.

## Requirements

- macOS or Linux
- Python 3
- Ollama
- one installed Ollama chat model
- **recommended: LOOK (`lk`)**
- optional `OLLAMA_API_KEY` for live web search

Future Crash uses Python's standard library only.

A good default model:

```bash
ollama pull qwen3:8b
```

A lighter option:

```bash
ollama pull qwen3:4b
```

## Run

```bash
python3 future_crash.py --model qwen3:8b
```

Check the exact file/version you launched:

```bash
python3 future_crash.py --version
```

## Launch Options

```text
--model MODEL       Ollama model used for AI work
--ollama URL        Ollama server address
--fps NUMBER        terminal refresh rate
--no-ai-ambient     disable ambient model observations
--no-audio          disable audio for this launch
--version           print version and exit
```

## Ambient Controls

```text
esc     drop into the real interactive shell
a       Quick Oracle
x       Workstation
t       Threads
f       fortune
r       observation
s       clear Signal drawing
d       Signal demo
m       mute / unmute sound
? / h   help
p       panic
q       guarded quit
```

The command footer wraps by complete menu item on narrow terminals.

### Shell handoff

`Esc` from Ambient restores the real terminal and launches `$SHELL -i`.
Your normal aliases, functions, prompt, zoxide, git, LOOK, and other shell tools
behave normally.

Type `exit` or press `Ctrl-D` to return to the same Future Crash process.

## Audio

Future Crash synthesizes small WAV cues and uses:

- macOS: `afplay`
- Linux: `aplay`

Press `m` at runtime to mute/unmute. The preference persists in:

```text
~/.future_crash/config.json
```

`--no-audio` overrides the saved preference for that launch.

## Quick Oracle

Press `a`.

Quick Ask sees persistent memory but does not itself write new memories.

## Workstation

Press `x`.

```text
enter       send
ctrl-t      Threads
ctrl-u      clear current conversation; persistent memory remains
ctrl-k      guarded erase of persistent memory
esc         return to Ambient
```

## Memory

Persistent memory uses six conceptual slots:

- one rolling compressed long memory
- five recent completed Workstation exchanges

When the five recent slots fill, the selected Ollama model compresses them with
the previous long memory into a refreshed long-memory summary.

## Web Search

When `OLLAMA_API_KEY` exists in the process environment, Future Crash exposes
hosted Ollama web search and reports:

```text
WEB        READY
```

Otherwise:

```text
WEB        NO KEY
```

Web search is informational and does not require a mutation approval dialog.

## Host Tools / Authority

The model may propose operations such as:

- list/read/find files
- create directories
- write/append files
- run approved commands
- open files or URLs

Consequential operations follow one rule:

```text
model proposes
→ operator approves
→ host executes
→ host verifies
→ HOST RECEIPT
→ model continues
```

The model does not get to claim an operation succeeded without the receipt.

## Threads

Threads are recurring Future Crash tasks stored in:

```text
~/.future_crash/tasks.json
```

A Thread contains one exact approved action, one interval, and one purpose.
Threads run while Future Crash itself is running.

Open the manager with `t` from Ambient or `ctrl-t` from Workstation.

The special action:

```json
{"name":"model_wake"}
```

exists for recurring model-only activity such as Signal art, fortunes, notes,
moods, or tiny autonomous status displays.

Example:

> Start a Thread called Signal Art. Every three minutes, make a new little
> piece of Signal Field art. Keep it varied and usually stay textually silent.

## Signal Field

The Signal Field is a shared model-controlled drawing/status surface.

The model has host-rendered primitives for text, lines, boxes, fills, circles,
ellipses, arrows, plots, and direct character placement. Ordinary drawings are
ephemeral. Thread-owned drawings can persist between Thread wakes.

`d` proves the renderer with a deterministic demo. `s` clears the current
deliberate drawing.

## LOOK Detection

Future Crash automatically detects an independently installed `lk` on `PATH` and reports `LOOK READY`; otherwise it reports `LOOK OPTIONAL`. No LOOK code is bundled into Future Crash.

## Configuration / State

Future Crash keeps its own small state under:

```text
~/.future_crash/
    config.json
    tasks.json
    tools/
    logs/
    task_state/
```

Persistent memory is stored separately in:

```text
~/.future_crash_memory.json
```

## Help

Press `?` or `h` from Ambient for the canonical in-app command reference.

---

*Please remain calm. The computer is attempting the same thing.*


## v0.9.8 — Help Paging

The in-app Help screen now scrolls instead of clipping on shorter terminals.

Controls:

    ↑ / ↓
    J / K       line scroll
    PgUp/PgDn   page
    Space       page down
    Home / G    top
    Esc / ? / H / Q   return

The footer shows the visible help range, e.g.:

    9-24/31

No other behavior changed.


## v0.9.8 — Key-label polish

Displayed command keys now use the actual unshifted keystrokes accepted by the
program: `[a]`, `[x]`, `[t]`, `[m]`, `[q]`, `ctrl-t`, `esc`, etc.

Interface names and status typography remain uppercase where appropriate.
Behavior is unchanged; uppercase keypresses continue to work.
