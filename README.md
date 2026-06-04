# VoxRT wake-word model weights

Pre-compiled wake-phrase detection model weights in **`.vxrt`**
format, packaged for the **VoxRT** on-device inference runtime.
Detects the phrase **"Hey Assistant"**.

Pair with one of the consumer libraries:

- Android — [`voxrt-wake-word-android`](https://github.com/VoxRT/voxrt-wake-word-android)
- iOS — [`voxrt-wake-word-ios`](https://github.com/VoxRT/voxrt-wake-word-ios)

This repo is a thin distribution layer — the actual files live as
GitHub Release attachments per version, not in the git tree. The
README below is the index.

---

## What is a `.vxrt` file?

A self-contained, binary, framework-agnostic model file:

- **Topology + weights** encoded in a compact format (no ONNX /
  PyTorch dependency at consume time).
- **AES-256-GCM encrypted** at rest, decrypted on load by the
  runtime ([ADR-0023](https://github.com/VoxRT/voxrt-wake-word-android#license)).
- **Versioned** — newer `.vxrt` files may add encoded features
  that older runtimes refuse to load; check the version
  compatibility table below.

You don't need to know the format to use it — feed the bytes to
`VoxrtWakeWordEngine` and it Just Works.

## Downloads

### v0.1.0

| File | Size | SHA-256 |
| ---- | ---- | ------- |
| [`voxrt_wake_word.vxrt`](https://github.com/VoxRT/voxrt-wake-word-models/releases/download/v0.1.0/voxrt_wake_word.vxrt) | 101K | `9d40bdc132a2ad8e85bd8a28bb49b77c51a7c62f60567222a037e44418510e8f` |

**Compatible with:** `VoxRT/voxrt-wake-word-ios@v0.1.0`,
`VoxRT/voxrt-wake-word-android@v0.1.0`.

## Model quality

Test split: 5,240 positive utterances + 6,416 hard-negative
utterances (isolated "Hey", isolated "Assistant", competitor
wake-words like "Hey Siri", phonetic neighbours, arbitrary
speech, non-speech audio). All speakers disjoint from train + val.

- **ROC AUC: 0.9966**
- **Average precision (PR AUC): 0.9899**

At the recommended deploy threshold of **0.9**:

| Metric    | Test value |
| --------- | ---------- |
| Precision | 0.993      |
| Recall    | 0.982      |
| F1        | 0.987      |
| FPR       | 0.5 %      |

See the [`voxrt-wake-word-android`](https://github.com/VoxRT/voxrt-wake-word-android#model-quality)
README for the full threshold sweep + per-category false-positive
breakdown.

## How to use

```bash
curl -L -o voxrt_wake_word.vxrt \
  https://github.com/VoxRT/voxrt-wake-word-models/releases/download/v0.1.0/voxrt_wake_word.vxrt
# verify checksum
echo "9d40bdc132a2ad8e85bd8a28bb49b77c51a7c62f60567222a037e44418510e8f  voxrt_wake_word.vxrt" | shasum -a 256 -c
```

Then bundle (in `assets/` for Android, in Xcode resources for
iOS) or download at runtime — see the platform repos for code
examples.

## Provenance + license

The wake-phrase model is **trained entirely in-house** by Elephant
Enterprises LLC (d/b/a VoxRT) on **100% synthetic data** — TTS-
generated positive utterances ("Hey Assistant" in voice-cloned
variants), decomposed hard-negative categories (isolated keywords,
competitor wake-words, phonetic rhymes, onset-overlap words, non-
speech audio), augmented with real-world RIR + background-noise
sources at training time. No upstream model checkpoints, no
copyleft or attribution obligations on the weights themselves.

The `.vxrt` artefact is distributed under the **VoxRT proprietary
license** — see [`LICENSE`](LICENSE). Redistribution as part of an
unmodified `voxrt-wake-word-{ios,android}` library is permitted
without per-installation fees; reverse engineering or extracting
the unencrypted weights is not. Contact help@voxrt.com for custom
phrase models, multi-phrase detection, or licensing terms beyond
the redistribution allowance.

## Architecture

- 8-block depthwise-separable Conv1D encoder with dilations
  `[1, 2, 4, 4, 4, 2, 2, 1]`, 64 channels, ~48K parameters total
- 64-bin Slaney-norm mel frontend, 16 kHz mono PCM input
- Global average pooling over 200-frame (2 s) sliding window,
  linear head, sigmoid output → wake-phrase confidence
- fp16 weights with AES-GCM at-rest encryption (~100 KB on disk)

Per-frame inference latency on a Snapdragon 662 (Cortex-A73):
~210 µs, giving RTF ≈ 0.021 — well within an always-on power
budget.

## Versioning

A model release at `vX.Y.Z` is built to work with VoxRT runtime
`vX.Y.Z` and (typically) all earlier minor versions sharing the
same major. Breaking format changes bump the major. See the
[iOS](https://github.com/VoxRT/voxrt-wake-word-ios/releases) and
[Android](https://github.com/VoxRT/voxrt-wake-word-android/releases)
release notes for the exact compatibility per release.

## Links

- Android runtime: [voxrt-wake-word-android](https://github.com/VoxRT/voxrt-wake-word-android)
- iOS runtime: [voxrt-wake-word-ios](https://github.com/VoxRT/voxrt-wake-word-ios)
- ASR companion model weights: [voxrt-asr-models](https://github.com/VoxRT/voxrt-asr-models)
- VAD companion model weights: [voxrt-silero-models](https://github.com/VoxRT/voxrt-silero-models)
- VoxRT and the runtime story: [voxrt.com](https://voxrt.com)
