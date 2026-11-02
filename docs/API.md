# Speech synthesis · 0.1.0

`Import speech`. `SpeechVoices()` returns installed `SpeechVoice` snapshots (Identifier, Name, Language). `New SpeechPlayer()` is silent; `Speak(text, language = "")` explicitly queues an utterance, `IsSpeaking` observes it, `Stop()` cancels speech, and `Close()` is final/idempotent. Keep the player alive until speech ends. Uses AVSpeechSynthesizer rather than the deprecated NSSpeechSynthesizer. Never requests personal-voice authorization. Creation and playback operations require the main thread. Worker-thread destruction explicitly queues native stop/release to the main thread; keep the application loop alive for cleanup.

These native operations require macOS; `SpeechSupported()` returns False on Windows/Linux, and unsupported operations throw rather than silently emulating an Apple API. All six compiler targets are checked; native execution is verified on macOS arm64.

Inspired by [macoslib’s Cocoa examples](https://github.com/macoslib/macoslib); implemented independently against [Apple’s API](https://developer.apple.com/documentation/avfaudio/avspeechsynthesizer).
