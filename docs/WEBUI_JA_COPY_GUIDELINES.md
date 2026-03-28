# WebUI Japanese Copy Guidelines

## Overview

This document defines the Japanese copy policy for the Gradio WebUI in this
fork.

The goal is to improve readability for Japanese users without changing the
underlying inference behavior, parameter semantics, or existing compatibility.

## Motivation

The current Gradio WebUI mixes English UI labels with Japanese-facing features
such as the emoji palette. This makes the interface less approachable for users
who mainly operate the model in Japanese.

At the same time, over-translating technical terms can make inference settings
harder to map back to code, README examples, and known parameter names.

This fork therefore adopts a restrained localization style:

- general UI wording should be natural in Japanese
- inference parameter names should remain recognizable in English
- short Japanese clarification in parentheses is allowed when it improves
  usability

## Specification

### Scope

- This policy applies only to the Gradio WebUI defined in `gradio_app.py`.
- The change target is display text only.
- The following UI elements are in scope:
  - page title text
  - section headings
  - button labels
  - textbox / slider / dropdown / audio component labels
  - accordion labels
  - short helper descriptions shown in the UI, including component `info`

### Out of Scope

- Internal implementation names
- Runtime log message format emitted by inference internals
- Hugging Face repo ids
- Device / precision option values such as `cuda`, `cpu`, `bf16`, `fp32`
- Request field names passed to `SamplingRequest`
- CLI argument names and README command examples
- A full Japanese rewrite of validation errors or internal detail logs

### Copy Style Rules

- General-purpose UI wording SHOULD be translated into natural Japanese.
- Parameter names MUST NOT be translated into different canonical names.
- When clarification is useful, the UI MAY use the following format:
  - `English parameter name（short Japanese clarification）`
- Parenthetical clarification MUST stay short and must not redefine the
  parameter.
- UI copy MUST avoid excessive translation that obscures correspondence with
  existing technical terms.

### Naming Rules

- Keep canonical parameter names as-is for inference controls, including:
  - `CFG Guidance Mode`
  - `CFG Scale Text`
  - `CFG Scale Speaker`
  - `CFG Min t`
  - `CFG Max t`
  - `Context KV Cache`
  - `Truncation Factor`
  - `Rescale k`
  - `Rescale sigma`
  - `Speaker KV Scale`
  - `Speaker KV Min t`
  - `Speaker KV Max Layers`
- General labels may be localized more freely, including:
  - page heading
  - model load / unload buttons
  - helper text for runtime reuse
  - emoji palette instructions
  - reference audio upload label
  - generated audio output labels

### Examples

- `Text` -> `Text（入力テキスト）`
- `Reference Audio Upload (optional, blank = no-reference mode)` ->
  `Reference Audio Upload（任意、空欄で no-reference mode）`
- `Load Model` -> `モデルを読み込む`
- `Generate` -> `音声を生成`
- `CFG Scale Text` -> keep unchanged
- `Context KV Cache` -> keep unchanged or use
  `Context KV Cache（高速化）`
- `Speaker KV Scale` -> keep unchanged and add short Japanese helper text if
  needed

### Compatibility

- UI localization MUST NOT change any submitted values.
- UI localization MUST NOT change dropdown choices or emitted request values.
- Existing emoji palette behavior defined in `docs/WEBUI_EMOJI_PALETTE.md`
  remains unchanged.
- The same checkpoint paths, Hugging Face repo ids, and runtime settings MUST
  continue to work without modification.

## Constraints

- Keep changes localized to WebUI copy and related documentation.
- Do not add an i18n framework or new dependency for this v1 copy update.
- Do not rename public inference parameters in code.
- Do not introduce new settings, validation rules, or behavior changes as part
  of localization.
