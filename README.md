# Cutting-Edge-Voice-AI-
Built a comprehensive call analysis system using Python that processes YouTube audio and extracts key sales metrics in under 30 seconds.

Overview
Built a comprehensive call analysis system using Python that processes YouTube audio and extracts key sales metrics in under 30 seconds.
Technical Stack

Audio Processing: youtube-dl + pydub for download/preprocessing
Speech Recognition: Google Speech API (free tier compatible)
Sentiment Analysis: Hugging Face transformers with lightweight RoBERTa model
Speaker Diarization: Rule-based approach using keyword analysis + segment alternation

Key Features

Talk-time Ratio: Audio segmentation on silence detection, duration tracking per speaker
Question Counting: Regex patterns for question marks + common question structures ("how much", "what is", etc.)
Monologue Detection: Consecutive segment grouping by speaker with duration aggregation
Sentiment Analysis: Text chunking + transformer model with score aggregation
Speaker ID: Keyword-based classification (sales terms vs customer terms) + positional fallback
