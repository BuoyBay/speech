---
title: "speech typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["SpeechPlayer", "SpeechVoice"]
dependencies: []
symbols: ["SpeechPlayer", "SpeechVoice"]
related: ["api.md", "getting-started.md", "index.md"]
---

# speech typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## Speech functions

### SpeechSupported

`Public Function SpeechSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### SpeechVoices

`Public Function SpeechVoices() As Array Of SpeechVoice`

No parameters.

#### Returns

| Type |
| --- |
| `Array Of SpeechVoice` |

## SpeechVoice

`Public Class SpeechVoice`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Identifier` | `String` | Yes | No | — | — |
| `Name` | `String` | Yes | No | — | — |
| `Language` | `String` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(identifier As String, name As String, language As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `identifier` | `String` | `ByVal` | Required |
| `name` | `String` | `ByVal` | Required |
| `language` | `String` | `ByVal` | Required |

Returns: no value.

## SpeechPlayer

`Public Class SpeechPlayer`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `IsSpeaking` | `Boolean` | Yes | No | — | — |

### Constructor

`Public Sub Constructor()`

No parameters.

Returns: no value.

### Speak

`Public Sub Speak(text As String, language As String = "")`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |
| `language` | `String` | `ByVal` | `""` |

Returns: no value.

### Stop

`Public Sub Stop()`

No parameters.

Returns: no value.

### Close

`Public Sub Close()`

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.
