# 🎙️ Voice-Based Patient Risk Screening (NLP Fine-Tuned)

A prototype clinical support tool that records a patient's spoken response, transcribes it, and screens the transcript for signs of emotional distress or self-harm risk — combining a fine-tuned sentiment classifier with keyword-based detection to help flag cases for clinician review.

## Features

- **Custom fine-tuned sentiment model** — `distilbert-base-uncased` fine-tuned on a labelled sentence dataset to classify sentiment as positive or negative, with confidence scoring
- **In-browser audio recording** — record directly from the microphone via an embedded HTML/JavaScript widget, no extra tools required
- **Speech-to-text transcription** — converts recorded audio to text using Google Speech Recognition (via ffmpeg + SpeechRecognition)
- **Self-harm keyword detection** — cross-checks the transcript against a curated list of self-harm and suicide-related phrases
- **Sarcasm / mismatch flag** — flags cases where sentiment is strongly positive but self-harm keywords are still present, so a human can review the discrepancy
- **Actionable output** — prints a clear summary with sentiment result, detected keywords, and a recommended next step (e.g. therapy referral, crisis support contact)

## How it works

1. **Setup** — installs dependencies (`ffmpeg`, `SpeechRecognition`, `torch`, `transformers`, `datasets`, `scikit-learn`) and mounts Google Drive for dataset access
2. **Model training** — loads a labelled sentiment dataset, fine-tunes DistilBERT as a text classifier using Hugging Face's `Trainer` with early stopping, evaluates accuracy/precision/recall/F1, and saves the model, tokenizer, and label encoder
3. **Audio capture** — displays Start/Stop recording buttons in the notebook; audio is recorded from the browser microphone and saved locally
4. **Transcription** — the recorded audio is converted to WAV and transcribed to text
5. **Risk analysis** — the transcript is run through:
   - the fine-tuned sentiment model (flags negative sentiment above a 60% confidence threshold)
   - a keyword scan against a list of self-harm/suicide-related phrases
   - a sarcasm check comparing sentiment polarity against keyword hits
6. **Output** — prints the transcript, sentiment result, any flagged keywords, and a recommended action

## Tech Stack

Python · PyTorch · Hugging Face Transformers · Datasets · scikit-learn · SpeechRecognition · ffmpeg · Google Colab

## ⚠️ Disclaimer

This notebook is a **prototype / research tool** and is **not a validated diagnostic or clinical instrument**. Its keyword list and sentiment thresholds have not been clinically calibrated, and outputs should never be used as a substitute for professional judgement. Any flagged result should be reviewed by a qualified clinician before any action is taken. If you or someone you know is in crisis, contact a crisis line such as Lifeline (13 11 14 in Australia) immediately.

## Collaborators

_Add collaborator names/links here if applicable._
