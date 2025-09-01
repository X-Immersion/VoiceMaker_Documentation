# VoiceMaker Unreal Plugin Documentation

Welcome to the VoiceMaker Unreal Plugin documentation. This plugin provides local text-to-speech (TTS) functionality for Unreal Engine, allowing you to generate high-quality speech audio directly within your project without requiring internet connectivity or external services.

## Features

- **Local TTS Generation**: Generate speech audio entirely offline using ONNX models
- **Multiple Voice Support**: Access to a wide variety of voices across different languages and genders
- **Runtime & Editor Support**: Generate TTS both at runtime and in the editor
- **Blueprint Integration**: Full Blueprint support with easy-to-use nodes
- **Audio Format Support**: Generate PCM, WAV data, or SoundWave assets
- **Asynchronous Processing**: Non-blocking audio generation with callback support
- *(upcoming)* **GPU offload generation**: Use the GPU to generate higher quality voices with low latency
- *(upcoming)* **Multiple architecture support**: Use the plugin with Linux and Mac, but also mobiles and consoles!

## Table of Contents

- [Voices](voices.md) - Available voices and their characteristics
- [Quickstart](quickstart.md) - Getting started with the plugin
  - [How to install the plugin through Fab and Epic Games launcher](quickstart.md#installation)
  - [How to use the plugin in editor (pre-generate TTS)](quickstart.md#editor-usage)
  - [How to use the plugin at runtime (runtime generated TTS)](quickstart.md#runtime-usage)
- [API Reference](api_reference.md) - Complete API documentation
  - [Config](api_reference.md#config) - Configuration settings
  - [Structs](api_reference.md#structs) - Data structures
    - [Voice Info](api_reference.md#voice-info)
    - [Audio Generation Result](api_reference.md#audio-generation-result)
  - [Enums](api_reference.md#enums) - Enumeration types
    - [Asset Conflict Resolution](api_reference.md#asset-conflict-resolution) *(editor only)*
  - [Classes](api_reference.md#classes) - Main classes and their methods
    - [VoiceMakerSubsystem](subsystem.md) - Core TTS subsystem
      - [Init](subsystem.md#init)
      - [Init (with settings)](subsystem.md#init-with-settings)
      - [Deinitialize](subsystem.md#deinitialize)
      - [Is Initialized](subsystem.md#is-initialized) *(pure)*
      - [Generate Audio Data](subsystem.md#generate-audio-data)
      - [Get Available Voices](subsystem.md#get-available-voices) *(pure)*
      - [Get Available Voices Info](subsystem.md#get-available-voices-info) *(pure)*
      - [Is Voice Available](subsystem.md#is-voice-available) *(pure)*
      - [Get Voice Information](subsystem.md#get-voice-information)
      - [Delegate - On Subsystem Error Occured](subsystem.md#on-subsystem-error-occured)
      - [Delegate - On Subsystem Status Changed](subsystem.md#on-subsystem-status-changed)
      - [Delegate - On Initialize Complete](subsystem.md#on-initialize-complete)
      - [Delegate - On Audio Data Generated Callback](subsystem.md#on-audio-data-generated-callback)
      - [Delegate - On Error Occured](subsystem.md#on-error-occured)
    - [VoiceMakerBPLibrary](bp_library.md) - Blueprint function library
      - [Initialize VoiceMaker Subsystem](bp_library.md#initialize-voicemaker-subsystem)
      - [Deinitialize VoiceMaker Subsystem](bp_library.md#deinitialize-voicemaker-subsystem)
      - [Is VoiceMaker Subsystem Initialized](bp_library.md#is-voicemaker-subsystem-initialized) *(pure)*
      - [Generate Audio Data](bp_library.md#generate-audio-data)
      - [Audio Data to PCM Data](bp_library.md#audio-data-to-pcm-data) *(pure)*
      - [Audio Data to WAV Data](bp_library.md#audio-data-to-wav-data) *(pure)*
      - [Create SoundWave from AudioData](bp_library.md#create-soundwave-from-audiodata)
      - [Save AudioData as SoundWave Asset](bp_library.md#save-audiodata-as-soundwave-asset) *(editor only)*
      - [Show save file selection dialog](bp_library.md#show-save-file-selection-dialog) *(editor only)*

## Requirements

- Unreal Engine 5.0 or later
- Windows, Mac, or Linux platform

## License

Copyright XandImmersion. All Rights Reserved.
