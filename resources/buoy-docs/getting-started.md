---
title: "Speech synthesis getting started"
summary: "Install speech and use its native API with explicit ownership."
category: "Guides"
order: 10
keywords: ["speech", "voices", "language", "synthesis"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

Install the sealed package in `packages/` and import `speech`. This example lists available voices without speaking. For a user-requested spoken action, retain a `SpeechPlayer` in the owning UI object and call `Speak(text)` or `Speak(text, language)` from the main thread. Do not create a short-lived player and immediately discard it after queuing an utterance.

```buoy
Import speech

Sub Main()
    If Not SpeechSupported() Then Exit Sub
    For Each voice As SpeechVoice In SpeechVoices()
        Print voice.Name + " (" + voice.Language + ")"
    Next
End Sub
```

## Handle native constraints

`SpeechSupported()` is a platform probe, so native voice enumeration or player construction can still throw if AV speech synthesis is unavailable. `Speak` rejects empty/whitespace-only text and closed players. A supplied language must have an installed supported voice or `InvalidArgumentException` is thrown. `Speak` queues work; returning does not mean the utterance has finished. `Stop()` cancels immediately. `IsSpeaking` returns False after close, and `Stop()` after close is a no-op.

[Package overview](index.md) · [API reference](api.md)
