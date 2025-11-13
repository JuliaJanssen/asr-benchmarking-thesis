# asr-benchmarking-thesis
This repository contains the code used for my master’s thesis on benchmarking nine off-the-shelf ASR models (AWS Transcribe, Whisper, and Wav2Vec 2.0) for Dutch medical and spontaneous speech.  
The code can be used for data preprocessing, transcript generation, and evaluation of ASR output.

## Datasets

This code was developed for use with following datasets:

-   [JASMIN](https://taalmaterialen.ivdnt.org/download/tstc-jasmin-spraakcorpus/)
-   [Common Voice](https://commonvoice.mozilla.org/nl/datasets)
-   [Primock57](https://github.com/babylonhealth/primock57)
-   [Homed Medicijnjournaal transcriptions](https://doi.org/10.34973/dpjc-0v85)
-   [AudioSet](https://research.google.com/audioset/download.html)
    

You will need to download these datasets yourself or adapt the code to work with your own data. File paths and structure will likely need adjustment.

## Environment Notes

Three notebooks were designed for use in an AWS SageMaker environment:

-   `transcribe.ipynb`
-   `wav2vec2.ipynb`
-   `whisper.ipynb`
    
These can be adapted for local or other cloud environments.  
AWS Transcribe is a hosted service and requires valid AWS credentials.

The notebook `mc-wer-en.ipynb` uses the Google Cloud Healthcare Natural Language API, which is deprecated and will be discontinued in May 2026. It is also a paid service.

`mc-wer-nl.ipynb` is based on [SaraSun01's repository](https://github.com/SaraSun01/thesis_closed_and_opened_ASR_comparison).

## Requirements
Two versions of requirements.txt are provided. Use `requirements.txt` if you are only using the preprocessing and/or analysis notebooks and `requirements-sagemaker.txt` if you are also using `transcribe.ipynb`, `wav2vec2.ipynb`, or `whisper.ipynb`.

`analyze results.ipynb` uses sclite (part of SCTK), which must be installed separately. Instructions can be found [here](https://github.com/usnistgov/SCTK).

## Repository Structure


| Folder                     | Description                                                                                                                                                                                |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `1. Audio/`     | Audio preprocessing: converting to .wav, 16kHz, mono (`process audio.ipynb`).                                                                                                                          
| `2. Reference/` | Reference transcript processing: conversion to .stm, digit mapping, punctuation cleanup, standardizing words (`commonvoice2stm.ipynb`, `jasmin2stm.ipynb`, `mj2stm.ipynb`, `cv_speaker_fix.ipynb`, `stm processing.ipynb`). |
| `3. Split/`     | Sentence-level audio splitting (`ja_split.ipynb`, `mj_split.ipynb`).                                                                                                                                     |
| `4. Selection/` | Dataset subset selection by demographics (`selection.ipynb`).                                                                                                                                            |
| `5. Models/`    | Hypothesis generation and analysis: ASR model scripts (`transcribe.ipynb`, `wav2vec2.ipynb`, `whisper.ipynb`) and results analysis (`analyze_results.ipynb`).                                            |
| `6. RQ1/`       | WER by demographic/accent group analysis (`jasmin bias.ipynb`, `common voice bias.ipynb`).                                                                                                                                     |
| `7. RQ2/`       | Hallucination and repetition detection (`hallucination.ipynb`).                                                                                                                                          |
| `8. RQ3/`       | Medical terminology analysis (`mc-wer-en.ipynb`, `mc-wer-nl.ipynb`).                                                                                                                                     |
| `9. RQ4/`       | Average processing time calculations (`processing_time.ipynb`).                                                                                                                                                                    |

## Disclaimer

This repository is provided as-is for research and educational purposes and is released under the MIT License. Some scripts rely on external datasets which are not included; users must download these datasets themselves and adapt file paths as needed. Certain scripts also use paid or deprecated services (e.g., AWS Transcribe, Google Cloud Healthcare API), whose availability and functionality may change. Users are responsible for complying with the licenses of any datasets or APIs they utilize.

## Contact
If you have questions about this code or would like to receive processed data, reference/hypothesis transcripts, or any analysis output, feel free to [contact me](mailto:github@juliajanssen.nl). 

A link to the thesis will be added once it is published.
