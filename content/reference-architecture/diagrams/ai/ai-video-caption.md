---
title: Automatic captioning for video uploads
pcx_content_type: reference-architecture-diagram
weight: 1
meta:
  title: "Reference Architecture Diagram: Automatic captioning for video uploads"
  description: By integrating automatic speech recognition technology into video platforms, content creators, publishers, and distributors can reach a broader audience, including individuals with hearing impairments or those who prefer to consume content in different languages.
tags:
  - AI
---

# Automatic captioning for video uploads

## Introduction

Automatic Speech Recognition (ASR) models have revolutionized the accessibility of video content by enabling the generation of subtitles and translations. These models utilize advanced algorithms to transcribe spoken words into text with high accuracy. By integrating ASR technology into video platforms, content creators, publishers, and distributors can reach a broader audience, including individuals with hearing impairments or those who prefer to consume content in different languages.

The process begins with capturing the audio from the video source, which is then fed into the ASR model. This model analyzes the audio waveform and converts it into a textual representation, capturing the spoken content in the form of subtitles. Furthermore, you can also use ASR models for language translation, enabling the creation of multilingual subtitles. Once the subtitles are generated, they can be displayed alongside the video, providing a synchronized text representation of the spoken content.

## Automatic captioning on upload

![Figure 1: Automatic captioning on upload](/images/reference-architecture/ai-auto-caption-architecture-diagrams/ai-auto-caption-architecture-diagram.svg "Figure 1:  Automatic captioning on upload")

1. **Client upload**: Send POST request with both video and audio to API endpoint.
2. **Audio transcription**: Generate timestamped transcriptions by calling [Workers AI](/workers-ai/) [automatic speech recognition (ARS) model](/workers-ai/models/#automatic-speech-recognition) with audio as input. Use [Workers](/workers/) to convert the output to a supported subtitled format.
3. **Store subtitles**: Store the subtitle file(s) on [R2](/r2/).
4. **Store video**: Store the video files on [R2](/r2/).
5. **Client request**: Send GET requests for video and subtitle(s) to origin. Use global [Cache](/cache/) to increase performance.
6. **Origin request**: Fetch file(s) from [R2](/r2/) on cache miss by using [Public Buckets](/r2/buckets/public-buckets/).

## Related resources

- [Community project: automatic captioning demo](https://auto-caption.pages.dev/)
- [Workers AI: Automatic speech recognition (ARS) model](/workers-ai/models/#automatic-speech-recognition)
- [R2: Object storage for all your data](/r2/)
