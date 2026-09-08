# Future Crash // Zero v0.9.3 — Input Guard / Signal Visibility

## Fixed: T hijacking Workstation typing
Plain T/t is now always ordinary text inside Workstation.

Open Threads from Workstation with:
    Ctrl-T

Ambient still uses plain:
    T

because Ambient has no text-entry conflict.

## Signal state visibility
The Signal canvas remains one shared `self.signal` object across Ambient,
Ask/Answer, and Workstation. Changing UI modes does not clear it.

A drawing disappears only when:
- its ordinary TTL expires
- another drawing clears/replaces it
- the operator presses S on Ambient
- a Thread that owns the persistent drawing is cancelled

Workstation's status line now exposes SIGNAL state, including the owning Thread
ID when a persistent Thread drawing is active. Signal panel titles also show
the Thread owner when applicable.

This makes it easier to distinguish:
- model did not actually emit a valid Signal block
from
- model drew successfully, but you're currently looking at another UI state.

Run:
    python3 future_crash.py --model qwen3:4b


## v0.9.3 — Model Wake Threads

A surgical addition for recurring model-only activity. Threads may now save
`{"name":"model_wake"}` as their exact action. It performs no host mutation;
it simply wakes the selected model on schedule and lets it carry out the
Thread purpose.

This makes recurring Signal art first-class:

    Start a Thread called Signal Art. Every three minutes, make a new little
    piece of Signal Field art. Keep it varied and usually stay textually silent.

The existing Thread scheduler, approval flow, persistence, Signal ownership,
and cancellation behavior are otherwise unchanged.
