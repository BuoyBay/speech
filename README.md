# macOS speech and voices

`Import speech`. `SpeechVoices()` returns installed `SpeechVoice` snapshots (Identifier, Name, Language). `New SpeechPlayer()` is silent; `Speak(text, language = "")` explicitly queues an utterance, `IsSpeaking` observes it, `Stop()` cancels speech, and `Close()` is final/idempotent. Keep the player alive until speech ends. Uses AVSpeechSynthesizer rather than the deprecated NSSpeechSynthesizer. Never requests personal-voice authorization. Creation and playback operations require the main thread. Worker-thread destruction explicitly queues native stop/release to the main thread; keep the application loop alive for cleanup.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add speech --git https://github.com/BuoyBay/speech.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
Import speech

Sub Main()
    If Not SpeechSupported() Then Exit Sub
    For Each voice As SpeechVoice In SpeechVoices()
        Print voice.Name + " (" + voice.Language + ")"
    Next
End Sub
```

## Platform and scope

Uses macOS AVSpeechSynthesizer. Voice discovery and speaking are separate operations; speaking is always an explicit application action.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer speech
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
