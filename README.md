# Whisper Local Speedbench

This Python script utilizes ffmpeg and OpenAI's Whisper model (local) to benchmark the transcription accuracy of audio files at various playback speeds. It speeds up audio files, transcribes them, and calculates the Word Error Rate (WER) from 1.1x to 4x speed increments. The normal 1.0x transcript serves as the baseline for accuracy comparison.

In this fork of the original project, we will keep initially ffmpeg to speed up the audio files. Yet, instead of using Whisper API, we will perform the transcription locally using the open source Whisper model.

There are some reasons for this choice:
  - Current Speedbench uses MP3 files to avoid hitting the 25 mb file size limit of they API.
  - Some users have reported that using MP3 instead of WAV files might impact the WER results.
  - Using WAV files will involve larger files and require chunking them to fit the API limits.
  - Chunking might lead to increased error rates due to errors during the merging phase of the transcriptions
  - Going local allows you to perform the task with larger files seamlessly
  - Keeping the same output format will allow us to compare new results to the existing benchmarks
  - In the future, it might allow us to compare several Whisper implementations, to see if the speed up process results in increased performance in other Whisper implementations like Faster Whisper, WhisperS2T, etc.

## Setup

1. **Environment Setup**:
   - Copy `example.env` to `.env` in the root directory and update it with your OpenAI API key:
     ```
     cp example.env .env
     # Open .env and replace your_openai_api_key_here with your actual OpenAI API key
     ```
   - Ensure the `.env` file is not tracked by Git (included in `.gitignore`).

2. **Install Dependencies**:
   ```
   pip install -r requirements.txt
   ```

## Usage
   - Execute the script by running:
     ```
     python benchmark.py path_to_your_audio_file
     ```
   - Optionally, specify the language code if the audio is not in English:
     ```
     python benchmark.py path_to_your_audio_file --language es
     ```

This script converts the specified audio file to MP3 format, processes it at speeds ranging from 1.1x to 4x, transcribes the audio using the Whisper API, computes the WER for each speed, and outputs the results to a CSV file named `benchmark_results.csv`.

## License

This project is licensed under the MIT License and is open-source.
