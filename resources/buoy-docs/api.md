---
title: "Speech synthesis API"
summary: "Public symbols and contracts for the speech package."
category: "Reference"
order: 20
keywords: ["speech", "voices", "language", "synthesis"]
symbols: ["SpeechSupported", "SpeechVoice", "SpeechVoices", "SpeechPlayer", "SpeechPlayer.Speak", "SpeechPlayer.IsSpeaking", "SpeechPlayer.Stop", "SpeechPlayer.Close"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

Import `speech` from the sealed package. The signatures below describe its public surface.

| Symbol | Contract |
| --- | --- |
| `SpeechSupported() As Boolean` | Report native backend support. |
| `SpeechVoices() As Array Of SpeechVoice` | Snapshot installed voices on the main thread. |
| `SpeechVoice.Identifier / Name / Language As String` | Read-only voice identity, display name, and language. |
| `New SpeechVoice(identifier, name, language)` | Construct a snapshot from String values. |
| `New SpeechPlayer()` | Create a silent synthesizer. |
| `Speak(text As String, language As String = "")` | Queue a nonempty utterance, optionally choosing a language. |
| `IsSpeaking As Boolean` | Read-only active-speech observation; False after close. |
| `Stop()` | Immediately cancel current speech; safe after close. |
| `Close()` | Permanently stop and release the synthesizer; repeated calls are safe. |

## Errors and lifecycle

`SpeechSupported()` is a platform probe, so native voice enumeration or player construction can still throw if AV speech synthesis is unavailable. `Speak` rejects empty/whitespace-only text and closed players. A supplied language must have an installed supported voice or `InvalidArgumentException` is thrown. `Speak` queues work; returning does not mean the utterance has finished. `Stop()` cancels immediately. `IsSpeaking` returns False after close, and `Stop()` after close is a no-op.

Enumerate voices and create/control players on the main thread. Keep a player alive until its speech ends. `Close()` is final and idempotent; destruction also retires native playback. Worker-thread destruction queues stop/release on the main thread, so keep the application loop alive while cleanup drains. Voice snapshots are ordinary read-only Buoy values.

## Platform support

Requires macOS. `SpeechSupported()` returns False on Windows and Linux; native voice enumeration and player construction throw on unsupported systems. Available voices depend on the installed system voices.

[Getting started](getting-started.md) · [Package overview](index.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
