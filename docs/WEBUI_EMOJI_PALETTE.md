# WebUI Emoji Palette

## Overview

This document defines the v1 emoji palette for the Gradio WebUI.

The palette exists only to assist text input in the WebUI. It does not change
the TTS model, the inference request format, or the meaning of any emoji.

Supported emoji semantics remain defined by `docs/EMOJI_ANNOTATIONS.md`.

## Motivation

The model supports speaking style, emotion, and sound effect control by
embedding emojis directly into the input text. While flexible, this requires the
user to remember which emoji corresponds to which effect.

The WebUI emoji palette improves discoverability and input speed while keeping
manual text entry fully compatible with the existing behavior.

## Specification

### Scope

- The feature applies only to the Gradio WebUI.
- The feature assists text entry only.
- The text submitted to inference remains plain text containing any inserted
  emojis verbatim.

### UI Placement

- The emoji palette MUST be displayed in an accordion near the main `Text`
  input.
- The accordion label MUST clearly indicate that it is for emoji input support.

### Grouping

The palette MUST group emoji buttons into the following categories:

- `感情`
- `話し方`
- `効果音・音声表現`

Each supported emoji MUST appear exactly once in one category.

### Item Format

Each palette item MUST display:

- the emoji itself
- a short Japanese label

The curated v1 labels are:

#### 感情

| Emoji | Label |
| --- | --- |
| 😭 | 泣き |
| 😱 | 悲鳴 |
| 😆 | 喜び |
| 😠 | 怒り |
| 😲 | 驚き |
| 😟 | 心配 |
| 🫣 | 恥ずかしさ |
| 🙄 | 呆れ |
| 😊 | 楽しげ |
| 🙏 | 懇願 |
| 🥴 | 酔い |
| 😌 | 安堵 |
| 🤔 | 疑問 |

#### 話し方

| Emoji | Label |
| --- | --- |
| 👂 | 囁き |
| 😏 | からかい |
| 🥺 | おどおど |
| 🫶 | 優しく |
| 😪 | 眠そう |
| ⏩ | 早口 |
| 🐢 | ゆっくり |
| 😰 | 慌て |
| 😖 | 苦しげ |

#### 効果音・音声表現

| Emoji | Label |
| --- | --- |
| 😮‍💨 | 吐息 |
| ⏸️ | 間 |
| 🤭 | 笑い |
| 🥵 | 喘ぎ |
| 📢 | エコー |
| 🌬️ | 荒い息 |
| 😮 | 息をのむ |
| 👅 | 舐める音 |
| 💋 | リップノイズ |
| 📞 | 電話越し |
| 🥤 | 飲み込み |
| 🤧 | 咳・くしゃみ |
| 😒 | 舌打ち |
| 🥱 | あくび |
| 👌 | 相槌 |
| 🎵 | 鼻歌 |
| 🤐 | 口塞がれ |

### Interaction

- Clicking a palette item MUST append exactly one emoji to the end of the
  current `Text` input value.
- Existing text MUST be preserved exactly as-is before the appended emoji.
- Repeated clicks MUST append repeated emojis in sequence at the end of the
  text.
- The implementation SHOULD keep focus on the text input when possible.

### Compatibility

- Manual emoji input in the `Text` input MUST continue to work unchanged.
- Repeated clicks on the same palette item MUST result in repeated emoji
  insertion.
- The inference pipeline MUST receive the textbox content exactly as shown to
  the user.

## Constraints

- v1 MUST NOT add emoji search.
- v1 MUST NOT add auto-conversion from aliases or keywords.
- v1 MUST NOT add warnings or validation for unsupported emojis.
- v1 MUST NOT add automatic intensity controls such as repeated insertion
  shortcuts.
- The feature MUST keep changes localized to the WebUI implementation.

## Examples

- Empty input + click `👂 囁き` -> `👂`
- `今日はいい天気です` + click `😊 楽しげ` -> `今日はいい天気です😊`
- `今日はいい天気です😊` + click `😭 泣き` -> `今日はいい天気です😊😭`
- Click `⏸️ 間` twice -> `⏸️⏸️`
