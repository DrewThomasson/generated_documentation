# Ebook to Audiobook Converter

Transform your eBooks into immersive audiobooks with optional custom Text-to-Speech (TTS) models.

This tool allows you to convert eBook files into audiobooks using TTS models. It supports multiple languages and allows the use of custom TTS models for personalized narration.

---

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Dependencies](#dependencies)
- [Usage](#usage)
  - [Running with Gradio Interface](#running-with-gradio-interface)
  - [Running in Headless Mode](#running-in-headless-mode)
- [Command Line Arguments](#command-line-arguments)
- [Examples](#examples)
- [Supported Languages](#supported-languages)
- [Troubleshooting and Common Issues](#troubleshooting-and-common-issues)
  - [Issue 1: Calibre's `ebook-convert` Not Found](#issue-1-calibres-ebook-convert-not-found)
  - [Issue 2: NLTK Data Not Found](#issue-2-nltk-data-not-found)
  - [Issue 3: FFmpeg Not Installed](#issue-3-ffmpeg-not-installed)
  - [Issue 4: Custom Model Not Loading](#issue-4-custom-model-not-loading)
  - [Issue 5: Out of Memory Errors](#issue-5-out-of-memory-errors)
  - [Issue 6: Slow Conversion Speed](#issue-6-slow-conversion-speed)
  - [Issue 7: Missing Audio Output](#issue-7-missing-audio-output)
  - [Issue 8: Errors Related to Torch or CUDA](#issue-8-errors-related-to-torch-or-cuda)
- [FAQ](#faq)
- [Acknowledgements](#acknowledgements)

---

## Features

- **Convert eBooks to Audiobooks**: Turn your eBook files into audiobooks using advanced TTS models.
- **Multi-Language Support**: Supports multiple languages for both the eBook content and TTS voices.
- **Custom TTS Models**: Option to use custom TTS models for personalized narration.
- **Headless Mode**: Run the tool directly from the command line without the need for a GUI.
- **Gradio Interface**: User-friendly web interface for easy interaction and configuration.
- **Adjustable TTS Parameters**: Customize TTS settings like temperature, speed, and repetition penalties.
- **Metadata and Cover Extraction**: Automatically extracts metadata and cover images from eBooks for enriched audiobooks.

---

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/ebook-to-audiobook-converter.git
cd ebook-to-audiobook-converter
```

### 2. Create a Virtual Environment (Optional but Recommended)

```bash
python3 -m venv venv
source venv/bin/activate  # For Windows, use `venv\Scripts\activate`
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

If a `requirements.txt` is not provided, you can manually install dependencies listed in the [Dependencies](#dependencies) section.

### 4. Install NLTK Data

The script uses NLTK's sentence tokenizer. Install necessary data:

```python
import nltk
nltk.download('punkt')
```

Or run:

```bash
python -m nltk.downloader punkt
```

### 5. Install Calibre

Calibre's `ebook-convert` tool is required.

- **Linux**:

  ```bash
  sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin
  ```

- **Windows/Mac**:

  Download and install from [Calibre's official website](https://calibre-ebook.com/download).

Ensure `ebook-convert` is in your system's PATH.

### 6. Install FFmpeg

FFmpeg is required for audio processing.

- **Linux**:

  ```bash
  sudo apt-get install ffmpeg
  ```

- **Windows/Mac**:

  Download from [FFmpeg's official website](https://ffmpeg.org/download.html) and add it to your system's PATH.

---

## Dependencies

- **Python Packages**:

  - `argparse`
  - `nltk`
  - `pydub`
  - `ebooklib`
  - `beautifulsoup4`
  - `tqdm`
  - `gradio`
  - `torch`
  - `TTS` (Coqui TTS)
  - `torchaudio`

- **Standard Libraries**:

  - `os`
  - `sys`
  - `re`
  - `subprocess`
  - `urllib.request`
  - `zipfile`
  - `socket`
  - `tempfile`

- **External Tools**:

  - **Calibre's `ebook-convert`**
  - **FFmpeg**

Install Python packages using:

```bash
pip install argparse nltk pydub ebooklib beautifulsoup4 tqdm gradio torch TTS torchaudio
```

---

## Usage

### Running with Gradio Interface

Launch the Gradio web interface:

```bash
python app.py
```

Output:

```
Running on local URL: http://localhost:7860
```

Open the provided URL in your web browser.

#### Interface Overview

- **eBook File**: Upload your eBook (e.g., `.epub`, `.mobi`, `.pdf`).
- **Target Voice File (Optional)**: Provide an audio sample to mimic the voice.
- **Language**: Select the language of the eBook and narration.
- **Use Custom Model**: Enable to use a custom TTS model.
  - **Custom Model File**: Upload `.pth` file.
  - **Custom Config File**: Upload `config.json`.
  - **Custom Vocab File**: Upload `vocab.json_`.
  - **Custom Model Zip URL**: URL to download the custom model as a zip file.
- **Audio Generation Preferences**: Adjust TTS parameters.
- **Convert to Audiobook**: Start the conversion.
- **Conversion Status**: Displays progress.
- **Audiobook Player**: Listen to the generated audiobook.
- **Download Audiobook Files**: Download the audiobook.

### Running in Headless Mode

Run the script directly from the command line:

```bash
python app.py --headless --ebook path_to_ebook [options]
```

#### Example

```bash
python app.py --headless --ebook mybook.epub --language en --temperature 0.7
```

---

## Command Line Arguments

| Argument                 | Type    | Description                                                                                                                      | Required |
|--------------------------|---------|----------------------------------------------------------------------------------------------------------------------------------|----------|
| `--share`                | `bool`  | Enable a public shareable Gradio link. Defaults to `False`.                                                                      | No       |
| `--headless`             | `bool`  | Run in headless mode without the Gradio interface. Defaults to `False`.                                                          | No       |
| `--ebook`                | `str`   | Path to the eBook file for conversion. **Required in headless mode.**                                                            | Yes      |
| `--voice`                | `str`   | Path to the target voice file for TTS. Uses default voice if not provided.                                                       | No       |
| `--language`             | `str`   | Language code for the audiobook conversion. Defaults to `en`.                                                                    | No       |
| `--use_custom_model`     | `bool`  | Use a custom TTS model. Defaults to `False`.                                                                                     | No       |
| `--custom_model`         | `str`   | Path to the custom model file (`.pth`). Required if using a custom model.                                                        | Yes\*    |
| `--custom_config`        | `str`   | Path to the custom config file (`config.json`). Required if using a custom model.                                                | Yes\*    |
| `--custom_vocab`         | `str`   | Path to the custom vocab file (`vocab.json_`). Required if using a custom model.                                                 | Yes\*    |
| `--custom_model_url`     | `str`   | URL to download the custom model as a zip file. Optional but used if provided.                                                   | No       |
| `--temperature`          | `float` | Temperature for the model. Defaults to `0.65`.                                                                                   | No       |
| `--length_penalty`       | `float` | Length penalty applied to the decoder. Defaults to `1.0`. Not applied to custom models.                                          | No       |
| `--repetition_penalty`   | `float` | Penalty to prevent repetition. Defaults to `2.0`.                                                                                | No       |
| `--top_k`                | `int`   | Top-k sampling. Lower values increase speed. Defaults to `50`.                                                                   | No       |
| `--top_p`                | `float` | Top-p sampling. Lower values increase speed. Defaults to `0.8`.                                                                  | No       |
| `--speed`                | `float` | Speech speed factor. Defaults to `1.0`.                                                                                          | No       |
| `--enable_text_splitting`| `bool`  | Enable splitting text into sentences. Defaults to `False`.                                                                       | No       |

\* Required if `--use_custom_model` is `True` and `--custom_model_url` is not provided.

---

## Examples

### Example 1: Basic Conversion

```bash
python app.py --headless --ebook mybook.epub --language en
```

Converts `mybook.epub` to an audiobook in English using default settings.

### Example 2: Using a Custom Voice

```bash
python app.py --headless --ebook mybook.epub --voice myvoice.wav --language en
```

Uses `myvoice.wav` as the target voice.

### Example 3: Using a Custom TTS Model

```bash
python app.py --headless --ebook mybook.epub --language en --use_custom_model True --custom_model_url "https://example.com/model.zip"
```

Downloads and uses a custom TTS model from the provided URL.

### Example 4: Adjusting TTS Parameters

```bash
python app.py --headless --ebook mybook.epub --language en --temperature 0.8 --speed 1.5 --top_k 40 --top_p 0.7
```

Customizes TTS parameters for different output characteristics.

---

## Supported Languages

- **English** (`en`)
- **Spanish** (`es`)
- **French** (`fr`)
- **German** (`de`)
- **Italian** (`it`)
- **Portuguese** (`pt`)
- **Polish** (`pl`)
- **Turkish** (`tr`)
- **Russian** (`ru`)
- **Dutch** (`nl`)
- **Czech** (`cs`)
- **Arabic** (`ar`)
- **Chinese (Simplified)** (`zh-cn`)
- **Japanese** (`ja`)
- **Hungarian** (`hu`)
- **Korean** (`ko`)

---

## Troubleshooting and Common Issues

### Issue 1: Calibre's `ebook-convert` Not Found

**Symptoms**: Error messages related to `ebook-convert` not being found.

**Possible Output**:

```
Error: Calibre's ebook-convert tool is not installed. Please install Calibre for this functionality.
```

**Solution**:

- Install Calibre as described in the [Installation](#installation) section.
- Ensure `ebook-convert` is in your system's PATH.
- Verify installation by running `ebook-convert --version`.

### Issue 2: NLTK Data Not Found

**Symptoms**: Errors related to NLTK's `punkt` tokenizer.

**Possible Output**:

```
LookupError:
**********************************************************************
  Resource punkt not found.
  Please use the NLTK Downloader to obtain the resource:
  >>> import nltk
  >>> nltk.download('punkt')
**********************************************************************
```

**Solution**:

- Run the following to download required NLTK data:

  ```python
  import nltk
  nltk.download('punkt')
  ```

- Or use:

  ```bash
  python -m nltk.downloader punkt
  ```

### Issue 3: FFmpeg Not Installed

**Symptoms**: Errors during audio processing or when creating M4B files.

**Possible Output**:

```
FileNotFoundError: [Errno 2] No such file or directory: 'ffmpeg'
```

**Solution**:

- Install FFmpeg as described in the [Installation](#installation) section.
- Ensure FFmpeg is in your system's PATH.
- Verify installation by running `ffmpeg -version`.

### Issue 4: Custom Model Not Loading

**Symptoms**: Errors when attempting to use a custom TTS model.

**Possible Output**:

```
FileNotFoundError: Custom model files not found.
```

**Solution**:

- Ensure all required files (`model.pth`, `config.json`, `vocab.json_`) are provided.
- If using a URL, verify it's correct and accessible.
- Check compatibility with the Coqui TTS version used.

### Issue 5: Out of Memory Errors

**Symptoms**: The script crashes with memory errors during conversion.

**Possible Output**:

```
RuntimeError: CUDA out of memory.
```

**Solution**:

- Close other applications to free up memory.
- Reduce batch sizes or adjust TTS parameters.
- Run on a system with more RAM.

### Issue 6: Slow Conversion Speed

**Symptoms**: Conversion takes an excessively long time.

**Solution**:

- Lower `top_k` and `top_p` values to increase speed.
- Disable unnecessary features like `enable_text_splitting`.
- Ensure your system meets the recommended specifications.

### Issue 7: Missing Audio Output

**Symptoms**: Conversion completes but no audiobook is generated.

**Possible Output**:

```
Audiobook created at ./Audiobooks/mybook.m4b
```

But the file is not present.

**Solution**:

- Verify the output directories (`Audiobooks`, `Chapter_wav_files`).
- Check for permission issues.
- Review console output for errors.

### Issue 8: Errors Related to Torch or CUDA

**Symptoms**: Errors like `CUDA out of memory` or `Torch not found`.

**Solution**:

- Ensure PyTorch is installed with the appropriate CUDA support.
- To force CPU usage, set:

  ```python
  device = torch.device("cpu")
  ```

- Or set the environment variable:

  ```bash
  export CUDA_VISIBLE_DEVICES=""
  ```

---

## FAQ

### Q1: Can I convert any eBook format?

**A**: Yes, the tool uses Calibre's `ebook-convert`, which supports various formats like EPUB, MOBI, PDF, etc.

### Q2: How do I change the voice used in the audiobook?

**A**: Provide a voice sample using the `--voice` argument or in the Gradio interface. The TTS model will mimic the provided voice.

### Q3: What do the TTS parameters do?

**A**: TTS parameters like Temperature, Top-k, and Top-p affect the randomness and creativity of the generated speech.

- **Temperature**: Higher values produce more varied outputs.
- **Top-k**: Limits the selection to the top k probable words.
- **Top-p**: Limits the selection to a cumulative probability.

### Q4: Can I use my own TTS model?

**A**: Yes, enable `--use_custom_model` and provide the necessary files or a download URL.

### Q5: Where are the generated audiobooks saved?

**A**: By default, in the `Audiobooks` directory within the script's working directory.

---

## Acknowledgements

- **[Coqui TTS](https://github.com/coqui-ai/TTS)**: Used for text-to-speech synthesis.
- **[Gradio](https://gradio.app/)**: For creating the web interface.
- **[Calibre](https://calibre-ebook.com/)**: For eBook conversion and metadata extraction.
- **[NLTK](https://www.nltk.org/)**: For sentence tokenization.

---

## Sample Program Output

When running the script, you might see outputs like:

```
starting...
Device selected is: cuda
Running on local URL: http://localhost:7860
Running on local URL: http://localhost:7860
```

During conversion:

```
Downloading Model: 100%|██████████| 200M/200M [00:20<00:00, 10MB/s]
Extracting Files: 100%|██████████| 3/3 [00:01<00:00,  2.00file/s]
All required files (model.pth, config.json, vocab.json_) found.
Creating chapter-labeled book
Converted chapter 1 to audio.
Converted chapter 2 to audio.
Creating M4B from chapters
Combined audio saved to ./Audiobooks/mybook.m4b
Audiobook created at ./Audiobooks/mybook.m4b
```

---

By following this guide, you should be able to successfully convert your eBooks into audiobooks and troubleshoot any issues that arise during the process.
