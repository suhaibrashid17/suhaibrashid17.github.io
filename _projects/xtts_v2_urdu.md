---
layout: page
title: XTTS-v2 for Urdu
description: A fine-tuned text-to-speech and voice-cloning model for Urdu, built on Coqui XTTS-v2.
img: assets/img/xtts-v2-urdu.png
importance: 2
---

Open-source text-to-speech models handle Urdu poorly, and voice cloning in Urdu is rarer still. I fine-tuned **XTTS-v2**, a multilingual voice-cloning TTS model, on Urdu speech so that it can read Urdu text in the voice of a short reference recording.

[Model on Hugging Face](https://huggingface.co/suhaibrashid17/XTTS-v2-Urdu-FT){: .highlight} · [Code on GitHub](https://github.com/suhaibrashid17/XTTS-v2-Urdu){: .highlight}

## What it does

Give the model Urdu text and a short audio sample of a speaker, and it generates Urdu speech in that speaker's voice. The model was fine-tuned on the **Common Voice Urdu** and **PRUS CSaLT** datasets.

## What I built

- **Fine-tuning.** I continued training XTTS-v2 on Urdu data. The released checkpoint has 17 epochs of training, and the loss was still decreasing, so further training should improve it.
- **Urdu tokenizer.** I changed the model's tokenizer so it handles Urdu text, and shipped it with the model.
- **Training and inference notebooks.** The repository includes notebooks to reproduce the fine-tuning and to run the model.
- **Public release.** The model is on Hugging Face with a usage guide and generated audio examples next to the source voices.

## Limitations

The model works best on short inputs and can degrade on very long text, so longer passages should be split into sentences first.
