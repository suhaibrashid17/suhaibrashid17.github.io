---
layout: page
title: Urdu-English Multimodal Toxic Language Detection
description: A real-time conversational Urdu audio dataset and models for toxicity detection beyond text.
img: assets/img/urdu-toxicity.png
importance: 1
---

Most toxicity classifiers work on text. For low-resource languages like Urdu this is a weak link: speech recognition (ASR) systems struggle with underrepresented toxic words, noisy and overlapping conversational audio, and real-world speech that differs from the controlled recordings they were trained on. Poor transcripts then lead to poor classification. This project, my undergraduate final-year project, instead classifies toxicity directly from **audio**.

## The problem with existing data

Meta's MuTox is the only audio-based toxicity dataset available for Urdu, but it has biased labeling (for example, Quranic and Biblical verses labeled as toxic) and is dominated by religious content. There was no real-time, conversational dataset for toxicity detection, so we built one.

## Dataset

2,466 audio clips in four categories, with 1,252 toxic and 1,214 non-toxic clips. Every clip was validated by all three team members.

| Category        | Toxic | Non-toxic | Data source                         |
| --------------- | ----: | --------: | ----------------------------------- |
| Vulgar          |   330 |       290 | TikTok live streams                 |
| Religious hate  |   315 |       320 | Islamic scholars                    |
| Political hate  |   298 |       307 | Talk shows                          |
| Racist          |   309 |       297 | YouTube creators and self-recorded  |

## Experiments

- **LLMs on transcripts.** We prompted two large LLMs (Llama 3.3 70B, DeepSeek-V3), one mid-size model (Gemma 2 27B) and two small ones (Gemma 2 9B, Llama 3.1 8B) with the same toxicity definition and asked for a toxic/non-toxic label with a one-line reason. Gemma 2 27B performed best of the LLMs.
- **Trained models.** We trained multilingual BERT and XLM-RoBERTa on text, ResNet-50 on audio, and a multimodal combination of Wav2Vec 2.0 audio features with mBERT.

| Model                 | Accuracy | Precision | Recall | F1     |
| --------------------- | -------: | --------: | -----: | -----: |
| Multilingual BERT     |   0.8011 |    0.7843 | 0.8421 | 0.8122 |
| XLM-RoBERTa           |   0.7903 |    0.8182 | 0.7579 | 0.7869 |
| ResNet-50 (audio)     |   0.8059 |    0.8058 | 0.8059 | 0.8055 |
| **Wav2Vec 2.0 + mBERT** | **0.8421** | **0.8521** | **0.8210** | **0.8362** |

## Takeaways

- Models trained specifically for toxicity classification outperform prompted LLMs.
- Combining audio and text gave the best results, and they are close to what state-of-the-art papers report for other languages (such as HateMM, MultiHateClip and ToxVidLM).
- Next steps: ASR evaluation, improving data quality, testing other model combinations from the literature, and integrating the best model into a product.
