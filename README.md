<img width="1350" height="845" alt="Screenshot 2026-09-02 at 8 27 13 PM" src="https://github.com/user-attachments/assets/bfb6bdfb-f074-4d86-b8a4-afcff2db176c" />


# FUTURE CRASH // ZERO

**A local AI workstation disguised as a slightly haunted 1980s
terminal.**

Future Crash is a dependency-light terminal companion built around a
local Ollama model. It combines an ambient retro-computer dashboard with
a quick Oracle, a full conversational Workstation, persistent memory,
web search, permissioned access to the host computer, recurring
background Threads, a tiny model-controlled Signal Field, telemetry,
glitches, synthesized bleeps, and occasional machine anxiety.

It is designed to feel less like a conventional chatbot and more like a
computer you leave running.

<img width="1350" height="852" alt="Screenshot 2026-09-02 at 8 29 12 PM" src="https://github.com/user-attachments/assets/2b30259f-c930-4fb3-bc90-baf48e55f71a" />


## Requirements

Future Crash is intentionally simple:

-   **macOS or Linux**
-   **Python 3**
-   **Ollama**
-   An Ollama model such as **Qwen3 8B**
-   Optional: an `OLLAMA_API_KEY` for live web search

The Python application itself uses the standard library and does not
require a Python package installation.

## 1. Install Ollama

Install Ollama from:

https://ollama.com/

Make sure Ollama is running, then download a model. Qwen3 8B is a good
default if your machine has enough memory:

``` bash
ollama pull qwen3:8b
```

A smaller model also works:

``` bash
ollama pull qwen3:4b
```

You can use other Ollama chat models as well.

## 2. Run Future Crash

From the directory containing `future_crash.py`:

``` bash
python3 future_crash.py --model qwen3:8b
```

Or with the smaller model:

``` bash
python3 future_crash.py --model qwen3:4b
```

The selected model is used for the Oracle, Workstation, ambient
observations, memory compression, Threads, and Signal Field
instructions.

## Launch Options

``` text
--model MODEL       Ollama model used for all AI work
                    Default: qwen3:4b

--ollama URL        Ollama server address
                    Default: http://127.0.0.1:11434

--fps NUMBER        Terminal UI refresh rate
                    Default: 12

--no-ai-ambient     Disable ambient AI observations

--no-audio          Disable synthesized terminal sounds
```

Example:

``` bash
python3 future_crash.py \
  --model qwen3:8b \
  --fps 12
```

## Live Web Search

Future Crash can use Ollama's hosted web search when an `OLLAMA_API_KEY`
is available in the environment.

For zsh:

``` bash
export OLLAMA_API_KEY="your-key-here"
```

You can put that line in `~/.zshrc` if you want it available
automatically in new terminal sessions.

Web search is used when a question requires current information;
ordinary conversation remains local.

## What It Does

### Ambient Terminal

The default screen is a living terminal dashboard with system telemetry,
fortunes, Oracle observations, the Signal Field, audio cues, glitches,
rare events, and occasional panic/recovery theater.

It is meant to be left running.

### Quick Oracle

Press **A** for a short, disposable conversation with the local model.

Quick Ask can read Future Crash's persistent memory, but does not itself
add new memories.

### Workstation

Press **X** for the full conversational Workstation.

The Workstation supports longer conversations, persistent context, host
tools, Threads, and the model-controlled Signal Field.

Inside Workstation:

``` text
Enter       Send
Ctrl-T      Open Threads
Ctrl-U      Clear the current conversation
Ctrl-K      Erase persistent memory (guarded)
Esc         Return to the ambient terminal
```

### Memory

Future Crash maintains a deliberately small persistent memory:

-   one compressed long-term memory
-   five recent completed Workstation exchanges

When the recent slots fill, the selected Ollama model compresses the
previous memory and recent exchanges into a refreshed long-term summary.

Clearing the current Workstation conversation does not erase persistent
memory.

### Host Tools and Authority

The model can work with the computer rather than merely talk about it.

It can propose operations such as:

-   listing and reading files
-   finding files
-   creating folders and files
-   appending text
-   running approved commands
-   opening files or URLs

Consequential operations require operator approval.

The execution model is intentionally strict:

> **Model proposes → operator approves → host executes → host verifies →
> HOST RECEIPT → model explains**

The model is never allowed to decide for itself that a computer
operation succeeded.

### Threads

Threads are persistent recurring tasks managed inside Future Crash.

A Thread can periodically repeat an approved action, inspect the
verified result, and report only when something meaningful changes.

Examples include:

-   checking a flight
-   watching a web page
-   monitoring a local process
-   periodically searching for new information

Press **T** from the ambient terminal, or **Ctrl-T** from Workstation,
to inspect Threads.

Threads currently run while Future Crash itself is running.

### Signal Field

The Signal Field is a tiny visual surface shared by the Oracle,
Workstation, and Threads.

The model can use it to create small diagrams, status displays, plots,
labels, geometric sketches, and persistent visual state. The host
performs the actual rasterization; the model describes what should be
drawn.

Thread-owned Signal displays can remain visible between Thread wakes.

From the ambient screen:

``` text
D           Show the deterministic Signal Canvas demo
S           Clear the current Signal drawing
```

## Audio

Future Crash synthesizes its own small WAV sound effects using Python's
standard library.

Playback uses the operating system's normal command-line audio player:

-   macOS: `afplay`
-   Linux: `aplay`

If audio is unavailable or unwanted:

``` bash
python3 future_crash.py --model qwen3:8b --no-audio
```

## Philosophy

Future Crash deliberately avoids becoming a large framework.

It is one Python program, one selected local model, one terminal, and a
small collection of host-side systems that give the model reliable
capabilities without pretending the model itself is the operating
system.

The terminal is the idle state.

The assistant is the machine underneath it.

------------------------------------------------------------------------

*FUTURE CRASH // Please remain calm. The computer is attempting the same
thing.*
