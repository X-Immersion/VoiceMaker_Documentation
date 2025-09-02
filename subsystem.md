# VoiceMakerSubsystem

[← Back to README](README.md) | [← Back to API Reference](api_reference.md)

## Table of Contents
- [Get Voice Maker Subsystem](#get-voice-maker-subsystem)
- [Init](#init)
- [Init (with settings)](#init-with-settings)
- [Deinitialize](#deinitialize)
- [Is Initialized](#is-initialized)
- [Generate Audio Data](#generate-audio-data)
- [Get Available Voices](#get-available-voices)
- [Get Available Voices Info](#get-available-voices-info)
- [Is Voice Available](#is-voice-available)
- [Get Voice Information](#get-voice-information)
- [On Subsystem Error Occured](#on-subsystem-error-occured)
- [On Subsystem Status Changed](#on-subsystem-status-changed)
- [On Initialize Complete](#on-initialize-complete)
- [On Audio Data Generated Callback](#on-audio-data-generated-callback)
- [On Error Occured](#on-error-occured)

<br/>

## Get Voice Maker Subsystem

**C++ Code**: `GEngine->GetEngineSubsystem<UVoiceMakerSubsystem>()`

![Get Subsystem menu](res/subsystem_menu_get.png)
![Get Subsystem](res/subsystem_get.png)

Get the VoiceMaker TTS Engine Subsystem

<br/>

## Init

**C++ Function**: `void UVoiceMakerSubsystem::InitializeLocalTTS(FOnInitializeComplete OnInitializeComplete, const FOnErrorOccured& OnErrorOccured)`

![Init Subsystem](res/subsystem_init.png)

Initialize the Local TTS engine with [project settings](api_reference.md#config) configuration.

> [!NOTE]
> Does nothing if the Subsystem is already initialized.

| Name | Type | Default Value | Description |
|------|------|---------------|-------------|
| OnInitializeComplete | [On Initialize Complete](#on-initialize-complete) | - | Called with `initialized=true` after the initialization is done |
| OnErrorOccured | const [On Error Occured](#on-error-occured)& | - | Called with `initialized=false` when the initialization failed |

<br/>

## Init (with settings)

**C++ Function**: `void UVoiceMakerSubsystem::InitializeLocalTTSWithSettings(const FString& ModelPath, const FString& VoicesPath, bool bUseGPU, FOnInitializeComplete OnInitializeComplete, const FOnErrorOccured& OnErrorOccured)`

![Init Subsystem with Settings](res/subsystem_init_settings.png)

Initialize the Local TTS engine with custom model files. This function loads the ONNX model and voice embeddings required for TTS generation.

> [!NOTE]
> Does nothing if the Subsystem is already initialized.

| Name | Type | Default Value | Description |
|------|------|---------------|-------------|
| ModelPath | `const FString&` | - | Path to the ONNX model file. Leave blank to use config model path |
| VoicesPath | `const FString&` | - | Path to the voices binary file. Leave blank to use config voice path |
| ~~bUseGPU~~ | `bool` | `false` | Whether to enable GPU acceleration (requires CUDA-compatible hardware) **(not supported yet)** |
| OnInitializeComplete | [On Initialize Complete](#on-initialize-complete) | - | Called with `initialized=true` after the initialization is done |
| OnErrorOccured | const [On Error Occured](#on-error-occured)& | - | Called with `initialized=false` when the initialization failed |

<br/>

## Deinitialize

**C++ Function**: `void UVoiceMakerSubsystem::DeinitializeLocalTTS(FOnInitializeComplete OnDeinitializeComplete)`

![Deinitialize Subsystem](res/subsystem_deinit.png)

Deinitialize the Local TTS engine.

> [!NOTE]
> Does nothing if the Subsystem is already deinitialized.

| Name | Type | Default Value | Description |
|------|------|---------------|-------------|
| OnDeinitializeComplete | [On Initialize Complete](#on-initialize-complete) | - | Called with `initialized=false` after the deinitialization is done |

<br/>

## Is Initialized

**C++ Function**: `bool UVoiceMakerSubsystem::IsInitialized() const`

![Is Initialized](res/subsystem_isinitialized.png)

Check if the TTS system is initialized and ready for audio generation.

**👉 Returns**: `bool` - True if the system is initialized and ready to generate audio

<br/>

## Generate Audio Data

**C++ Function**: `void UVoiceMakerSubsystem::GenerateAudioData(const FString& Text, const FString& VoiceName, float Speed, const FString& Language, FOnAudioDataGeneratedCallback OnComplete, const FOnErrorOccured& OnErrorOccured)`

![Generate Audio Data](res/subsystem_generate.png)

Generate audio data from text asynchronously. You can then use the following nodes with the [Audio Data](api_reference.md#audio-generation-result):
* [Audio Data to PCM Data](bp_library.md#audio-data-to-pcm-data)
* [Audio Data to WAV Data](bp_library.md#audio-data-to-wav-data)
* [Create SoundWave from AudioData](bp_library.md#create-soundwave-from-audiodata)
* [Save AudioData as SoundWave Asset](bp_library.md#save-audiodata-as-soundwave-asset) *(editor only)*

| Name | Type | Default Value | Description |
|------|------|---------------|-------------|
| Text | `const FString&` | - | The text to convert to speech |
| VoiceName | `const FString&` | - | Voice identifier. This **must** be the voice full name, i.e.: `af_alloy`. Empty = default voice. See [available voices](voices.md) |
| Speed | `float` | `1.0f` | Speech speed multiplier (0.5-2.0) |
| Language | `const FString&` | - | Language code, i.e.: `en_us`. Empty = default language |
| OnComplete | [On Audio Data Generated Callback](#on-audio-data-generated-callback) | - | Callback executed when generation succeeds, with the generated [Audio Generation Result](api_reference.md#audio-generation-result) |
| OnErrorOccured | const [On Error Occured](#on-error-occured)& | - | Callback executed when there was a generation error |

<br/>

## Get Available Voices

**C++ Function**: `TArray<FString> UVoiceMakerSubsystem::GetAvailableVoices() const`

![Get Available Voices](res/subsystem_getvoices.png)

Get all available voice identifiers. Returns a list of all voice names that can be used with the generation functions.

> [!CAUTION]
> This will return an empty array if the Subsystem is not initialized.

**👉 Returns**: `TArray<FString>` - Array of voice identifiers, i.e.: ["af_sarah", "am_adam", "bf_emma"]

<br/>

## Get Available Voices Info

**C++ Function**: `TArray<FVoiceInfo> UVoiceMakerSubsystem::GetAvailableVoicesInfo() const`

![Get Available Voices Info](res/subsystem_getvoiceinfo.png)

Get detailed information about all available voices. Provides [structured information](api_reference.md#voice-info) about each voice including display names, gender, language, and descriptions.

> [!CAUTION]
> This will return an empty array if the Subsystem is not initialized.

**👉 Returns**: `TArray<FVoiceInfo>` - Array of [Voice Info](api_reference.md#voice-info) structures

<br/>

## Is Voice Available

**C++ Function**: `bool UVoiceMakerSubsystem::IsVoiceAvailable(const FString& VoiceName) const`

![Is Voice Available](res/subsystem_isvoiceavailable.png)

Check if a specific voice is available. Use this to validate voice names before generation to avoid errors.

| Name | Type | Default Value | Description |
|------|------|---------------|-------------|
| VoiceName | `const FString&` | - | Voice identifier to check |

**👉 Returns**: `bool` - True if the voice is available for use

<br/>

## Get Voice Information

**C++ Function**: `FVoiceInfo UVoiceMakerSubsystem::GetVoiceInformation(const FString& VoiceName) const`

![Get Voice Information](res/subsystem_getvoiceinfo.png)

Get detailed information about a specific voice. Retrieves structured information about a specific voice by its identifier.

> [!CAUTION]
> This will return an empty voice if the Subsystem is not initialized.

| Name | Type | Default Value | Description |
|------|------|---------------|-------------|
| VoiceName | `const FString&` | - | Voice identifier to query |

**👉 Returns**: [Voice Info](api_reference.md#voice-info) - `FVoiceInfo` structure containing voice details, or empty if not found

<br/>

## Delegates

### On Subsystem Error Occured

**C++ Delegate**: `FOnSubsystemErrorOccured UVoiceMakerSubsystem::OnSubsystemErrorOccured`

![On Subsystem Error Occured](res/subsystem_onerror.png)

Delegate called every time an error occurred on the subsystem.

| Name | Type | Description |
|------|------|-------------|
| ErrorMessage | `const FString&` | The error message describing what went wrong |

<br/>

### On Subsystem Status Changed

**C++ Delegate**: `FOnSubsystemStatusChanged UVoiceMakerSubsystem::OnSubsystemStatusChanged`

![On Subsystem Status Changed](res/subsystem_onstatuschanged.png)

Delegate called every time the subsystem is initialized or deinitialized.

| Name | Type | Description |
|------|------|-------------|
| bInitialized | `bool` | True if the subsystem was initialized, false if deinitialized |

<br/>

### On Initialize Complete

**C++ Delegate**: `FOnInitializeComplete`

![On Initialize Complete](res/delegate_initcomplete.png)

Dynamic delegate called when initialization or deinitialization completes. Used with nodes [Init](#init), [Init (with settings)](#init-with-settings) and [Deinitialize](#deinitialize).

| Name | Type | Description |
|------|------|-------------|
| bInitialized | `bool` | True if initialization succeeded, false if it failed or was deinitialized |

<br/>

### On Audio Data Generated Callback

**C++ Delegate**: `FOnAudioDataGeneratedCallback`

![On Audio Data Generated](res/delegate_audiogenerated.png)

Dynamic delegate called when audio generation completes successfully. Used with node [Generate Audio Data](#generate-audio-data).

| Name | Type | Description |
|------|------|-------------|
| AudioData | [Audio Generation Result](api_reference.md#audio-generation-result) | The generated FAudioGenerationResult containing audio samples and metadata |

<br/>

### On Error Occured

**C++ Delegate**: `FOnErrorOccured`

![On Error Occured](res/delegate_error.png)

Dynamic delegate called when an error occurs during TTS operations. Used with nodes [Init](#init), [Init (with settings)](#init-with-settings) and [Generate Audio Data](#generate-audio-data).

| Name | Type | Description |
|------|------|-------------|
| ErrorMessage | `const FString&` | The error message describing what went wrong |
