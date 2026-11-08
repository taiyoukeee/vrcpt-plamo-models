# VRCPT PLaMo translation models

**Built with PLaMo**

This repository hosts the GGUF translation models that the VRC Power Translation (VRCPT) Android app downloads on the phone. The models are PLaMo 3 Translate by Preferred Networks, Inc., and run on-device with llama.cpp.

The model files are attached to this repository's **[Releases](../../releases)**. They are not committed to git.

## Models

| App step | File | Bytes | SHA-256 | Source |
|---|---|---:|---|---|
| 0.8B · medium | `plamo-3-translate-0.8b-Q4_K_M.gguf` | 573,123,200 | `923b2f28a9856de1b8b3b610a7e59ded0b14d007466fd5dd526e6a9ecaadafdd` | Official GGUF ([pfnet/plamo-3-translate-0.8b-GGUF](https://huggingface.co/pfnet/plamo-3-translate-0.8b-GGUF)) |
| 0.8B · high | `plamo-3-translate-0.8b-Q8_0.gguf` | 948,895,808 | `7797c44834adbfebdd3a1c85605e5655d96871f09fcfff009e9cd8b4e6723854` | Quantized from the official BF16 weights ([pfnet/plamo-3-translate-0.8b](https://huggingface.co/pfnet/plamo-3-translate-0.8b)) with llama.cpp b12125 |
| 2B · light (default) | `plamo-3-translate-2b-Q4_0.gguf` | 1,698,566,560 | `7a1839ed7f315b03176a7c7bb697629a95f8c3a61e669dfdf1cbeb6471551a66` | Official GGUF ([pfnet/plamo-3-translate-2b-GGUF](https://huggingface.co/pfnet/plamo-3-translate-2b-GGUF)) |
| 2B · medium | `plamo-3-translate-2b-Q4_K_M.gguf` | 1,807,199,392 | `f36d0813dd95573a852ab5d76e374c543632d9e292929e922bcdbf7e53b494e0` | Official GGUF ([pfnet/plamo-3-translate-2b-GGUF](https://huggingface.co/pfnet/plamo-3-translate-2b-GGUF)) |
| 2B · high | `plamo-3-translate-2b-Q8_0.gguf` | 3,061,858,912 | `2943b8b61683a3d86c03a2dc4221223b55928787d86836e9f1314a7f94af6002` | Quantized from the official BF16 weights ([pfnet/plamo-3-translate-2b](https://huggingface.co/pfnet/plamo-3-translate-2b)) with llama.cpp b12125 |

GitHub release assets are limited to 2 GiB each, so `plamo-3-translate-2b-Q8_0.gguf` is uploaded in two parts. Join them in order to get the file above.

| Part | Bytes | SHA-256 |
|---|---:|---|
| `plamo-3-translate-2b-Q8_0.gguf.part0` | 1,530,929,456 | `7f3a0bebbb17f826d568890a705a1e9cbaf4c8f529ec62026c96fab81aa96fee` |
| `plamo-3-translate-2b-Q8_0.gguf.part1` | 1,530,929,456 | `7006587c8f10b99c64827e7184531cf3e85cb5d39ebbe2d3236439a8fc2cf02b` |

`manifest.json` in each release lists the same data in machine-readable form for the app.

The Q8_0 files were made like this:

```
python llama.cpp/convert_hf_to_gguf.py <HF weights> --outtype bf16 --outfile <BF16.gguf>
llama-quantize <BF16.gguf> <Q8_0.gguf> Q8_0
```

## License

These models and their derivatives are provided under the **PLaMo Community License Agreement**. Copies are in [`LICENSE/`](LICENSE) ([English](LICENSE/PLaMo-Community-License-en.txt), [Japanese](LICENSE/PLaMo-Community-License-ja.txt)).

- By downloading or using these files, you agree to that license.
- Commercial use requires prior registration with Preferred Networks and is limited by revenue. See Article 3 of the license.
- This repository is not affiliated with or endorsed by Preferred Networks, Inc.

## Speech recognition models (release `asr-v1`)

The app also downloads per-language speech recognition models from the **`asr-v1`** release. They run on-device with [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) 1.13.8. The files are the official sherpa-onnx conversions, unchanged and only renamed with a model prefix. Korean keeps the SenseVoice model bundled in the app.

| Language | Model | License | Source | sherpa-onnx package |
|---|---|---|---|---|
| Japanese | ReazonSpeech k2 v2 (Zipformer transducer) | Apache-2.0 | [reazon-research/reazonspeech-k2-v2](https://huggingface.co/reazon-research/reazonspeech-k2-v2) | `sherpa-onnx-zipformer-ja-reazonspeech-2024-08-01` |
| English, Chinese | X-ASR zh-en with punctuation (Zipformer transducer) | Apache-2.0 | [Gilgamesh-J/X-ASR](https://github.com/Gilgamesh-J/X-ASR) | `sherpa-onnx-x-asr-zipformer-transducer-zh-en-punct-int8-2026-06-03` |
| Russian | GigaAM v3 with punctuation (NeMo transducer) | MIT | [salute-developers/GigaAM](https://github.com/salute-developers/GigaAM) | `sherpa-onnx-nemo-transducer-punct-giga-am-v3-russian-2025-12-16` |

Each model has four files: `encoder`, `decoder`, `joiner` and `tokens.txt`. `asr-manifest.json` lists every asset with its size and SHA-256. License texts: [Apache-2.0](LICENSE/Apache-2.0.txt), [GigaAM (MIT)](LICENSE/GigaAM-MIT.txt).
