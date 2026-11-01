---
title: "Speech synthesis"
summary: "Inspect installed voices and explicitly queue native speech."
category: "Overview"
order: 0
keywords: ["speech", "voices", "language", "synthesis"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Speech synthesis

The `speech` package uses `AVSpeechSynthesizer` for explicit spoken output and exposes installed voice snapshots. Creating a `SpeechPlayer` is silent. The package never requests personal-voice authorization.

## Platform support

Requires macOS. `SpeechSupported()` returns False on Windows and Linux; native voice enumeration and player construction throw on unsupported systems. Available voices depend on the installed system voices.

## Ownership and lifetime

Enumerate voices and create/control players on the main thread. Keep a player alive until its speech ends. `Close()` is final and idempotent; destruction also retires native playback. Worker-thread destruction queues stop/release on the main thread, so keep the application loop alive while cleanup drains. Voice snapshots are ordinary read-only Buoy values.

## Read next

- [Getting started](getting-started.md)
- [API reference](api.md)
