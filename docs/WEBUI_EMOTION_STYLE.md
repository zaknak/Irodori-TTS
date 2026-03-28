# WebUI Emotion Style Controls

## Overview

This document defines the `🎭 感情スタイル` accordion in the Gradio WebUI.

The accordion groups expression-oriented inference controls in one place
without changing backend parameter names or default inference behavior.

## Motivation

The WebUI currently spreads emotion- and style-related controls across
`Sampling` and `Advanced`, which makes it harder to understand which settings
mainly affect expression.

This fork adds a dedicated accordion so users can tune expressive behavior more
intuitively while preserving existing runtime semantics.

## Specification

### Scope

- This feature applies only to the Gradio WebUI in `gradio_app.py`.
- It reorganizes existing inference controls only.
- It does not add new backend fields or remove existing backend support.

### Accordion Placement

- The WebUI MUST add an accordion labeled `🎭 感情スタイル`.
- The accordion MUST appear before `Sampling`.
- `Sampling` MUST appear after `🎭 感情スタイル` and before `Advanced`.
- The reference audio upload UI MUST be wrapped in its own accordion.
- The reference audio accordion MUST appear immediately before the generate
  button.
- `Sampling` MUST keep only:
  - `Num Steps`
  - `Num Candidates`
  - `Seed`
  - `CFG Guidance Mode`

### Controls

The `🎭 感情スタイル` accordion MUST include the following controls.

#### CFG Scale Text（テキスト表現力）

- Backend field: `cfg_scale_text`
- Control type: slider
- Minimum: `0.0`
- Maximum: `10.0`
- Step: `0.1`
- Default: `3.0`
- Helper text MUST explain that increasing the value strengthens text-driven
  emotion and intonation, while decreasing it softens the response to the text.

#### CFG Scale Speaker（感情の強さ）

- Backend field: `cfg_scale_speaker`
- Control type: slider
- Minimum: `0.0`
- Maximum: `10.0`
- Step: `0.1`
- Default: `5.0`
- Helper text MUST explain that increasing the value strengthens the influence
  of the reference audio's emotion and speaking style, while decreasing it
  weakens that influence.

#### Speaker KV Scale（話者密着度）

- Backend field: `speaker_kv_scale`
- Control type: checkbox + slider
- Enable toggle default: OFF
- Slider minimum when enabled: `0.1`
- Maximum: `5.0`
- Step: `0.1`
- Slider default when enabled: `1.0`
- When the enable toggle is OFF, the UI MUST pass `None` to
  `SamplingRequest.speaker_kv_scale`.
- When the enable toggle is ON, the slider value MUST be passed through as-is.
- Helper text MUST mention both:
  - higher values increase closeness to the reference speaker
  - OFF means disabled

#### Truncation Factor（表現の振れ幅）

- Backend field: `truncation_factor`
- Control type: checkbox + slider
- Enable toggle default: OFF
- Slider minimum when enabled: `0.7`
- Maximum: `1.2`
- Step: `0.05`
- Slider default when enabled: `0.7`
- When the enable toggle is OFF, the UI MUST pass `None` to
  `SamplingRequest.truncation_factor`.
- When the enable toggle is ON, the slider value MUST be passed through as-is.
- Helper text MUST explain that lower values stabilize and flatten output,
  higher values increase expressive variation and momentum.

### Advanced Controls

- `Speaker KV Min t` and `Speaker KV Max Layers` MUST remain under `Advanced`.
- Their helper text SHOULD state that they are auxiliary controls used only when
  `Speaker KV Scale > 0`.

### Compatibility

- The feature MUST NOT change `SamplingRequest` field names.
- The feature MUST preserve existing backend parameter semantics.
- Initial UI values MUST produce the following backend values:
  - `cfg_scale_text=3.0`
  - `cfg_scale_speaker=5.0`
  - `speaker_kv_scale=None`
  - `truncation_factor=None`

## Constraints

- Keep parameter names recognizable in English.
- Use short Japanese explanations in labels or helper text.
- Do not move `CFG Guidance Mode` into `🎭 感情スタイル`.
- Do not change validation semantics in the inference runtime.
