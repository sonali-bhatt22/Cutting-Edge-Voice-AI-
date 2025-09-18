# Call Quality Analyzer

> A high-speed Python system to process YouTube audio from sales calls and extract key performance metrics in under 30 seconds, optimized for a Google Colab environment.

This project provides a comprehensive call analysis pipeline that takes a YouTube video URL, processes the audio, and generates actionable insights about the conversation, such as talk-time ratio, sentiment, and question frequency. The entire process is designed to be lightweight and efficient.

## Key Features

*   **Talk-Time Ratio:** Calculates the percentage of time each speaker is talking.
*   **Question Counting:** Identifies and counts the number of questions asked by each participant.
*   **Monologue Detection:** Flags long, uninterrupted segments of speech by a single speaker.
*   **Sentiment Analysis:** Assigns a sentiment score (positive, negative, neutral) to the conversation.
*   **Speaker Identification:** Differentiates between the sales representative and the customer.

## Technical Stack

*   **Audio Processing:** `youtube-dl` for downloading audio and `pydub` for preprocessing (silence splitting, format conversion).
*   **Speech-to-Text:** Google Speech Recognition API (leveraging its free-tier compatibility).
*   **Sentiment Analysis:** Hugging Face `transformers` with a lightweight, fine-tuned RoBERTa model for efficient sentiment scoring.
*   **Speaker Diarization:** A custom rule-based approach for speed and simplicity.

## How It Works

The system follows a multi-step pipeline to balance accuracy with performance:

1.  **Audio Ingestion:** Downloads the audio stream directly from a YouTube URL.
2.  **Audio Segmentation:** The audio is split into segments based on silence detection. This isolates individual speech chunks.
3.  **Transcription:** Each audio chunk is passed to the Google Speech API to generate a transcript.
4.  **Speaker Diarization:** A rule-based system identifies the speaker for each segment.
    *   **Keyword Analysis:** Classifies segments based on the presence of sales-specific terms ("pricing", "demo", "feature") versus customer-specific terms ("I need", "my problem is").
    *   **Alternating Segments:** Assumes speakers alternate in a typical conversation as a fallback logic.
5.  **Metric Extraction:**
    *   **Talk-Time & Monologues:** Aggregates the duration of consecutive segments from the same speaker.
    *   **Question Counting:** Uses regex patterns (`?`, "how much", "what is") to count questions in each speaker's transcript.
    *   **Sentiment Analysis:** The full transcript is chunked and fed into the RoBERTa model. The final sentiment is an aggregation of the chunk scores.

## Optimizations for Colab

The system was built with the constraints of the free Google Colab tier in mind:

*   **CPU-Only Processing:** All models and libraries are configured to run efficiently on CPU to avoid GPU memory limitations.
*   **Memory Efficiency:** Uses streaming for audio processing and cleans up temporary files immediately to manage disk space. Models are loaded once and reused.
*   **Chunked Analysis:** Long transcripts are broken into smaller pieces for sentiment analysis to prevent out-of-memory errors.
*   **Robust Error Handling:** Includes logic to manage poor audio quality, gracefully handling segments where speech cannot be clearly recognized.

## Performance

*   **Speed:** Processes a typical 5-10 minute sales call in **15-25 seconds**.
*   **Resilience:** Handles variations in audio quality by tuning silence detection thresholds and incorporating noise reduction during preprocessing.
*   **Accuracy:** The rule-based diarization and lightweight models provide a strong balance of accuracy and speed, suitable for high-level call analysis.
