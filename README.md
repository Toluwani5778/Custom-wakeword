# Wake Word Training Project

This repository is a hands-on workspace for experimenting with custom wake-word detection using OpenWakeWord. It includes notebooks for training models, testing pretrained models, generating synthetic data, and evaluating model performance.

The project is designed for local experimentation and learning, with a focus on creating and testing custom wake words such as "hey siri" or other phrases tailored to your own use case.

## Features

- Custom wake-word model training using OpenWakeWord
- Automated dataset generation and augmentation workflow
- Local inference testing from microphone input
- Export to ONNX/TFLite-friendly model formats
- Notebook-based exploration and experimentation
- Pretrained model testing and performance evaluation

## Project Structure

```text
.
├── README.md
├── requirements.txt
├── examples/
│   └── custom_model.yml
├── notebooks/
│   ├── Train_Your_First_Wake_Word_Model.ipynb
│   ├── automatic_model_training.ipynb
│   ├── training_models.ipynb
│   ├── performance_metrics.ipynb
│   ├── download_data.py
│   ├── train_model.py
│   ├── custom_model.yml
│   ├── my_model.yaml
│   ├── data/
│   ├── audioset/
│   ├── audioset_16k/
│   ├── fma/
│   ├── mit_rirs/
│   ├── models/
│   ├── my_custom_model/
│   ├── openwakeword/
│   ├── piper_models/
│   ├── piper-sample-generator/
│   ├── saved_model/
│   ├── validation_set_features.npy
│   └── ...
├── myenv/
└── .gitignore
```

## What This Repo Covers

This project is focused on the following workflow:

1. Prepare or download training data
2. Generate synthetic positive and negative wake-word examples
3. Configure model training parameters
4. Train a custom OpenWakeWord model
5. Export the trained model to ONNX/TFLite-compatible formats
6. Test detection locally from microphone input
7. Validate performance on negative and positive samples

## Recommended Workflow

### 1. Start with the beginner notebook

Use the notebook in `notebooks/Train_Your_First_Wake_Word_Model.ipynb` to:

- verify the OpenWakeWord package is installed correctly
- load a model
- test live microphone detection
- understand the wake-word scoring loop

This is the best first step if you want to quickly confirm that the environment and model pipeline are working.

### 2. Train a custom model

Use the notebook in `notebooks/automatic_model_training.ipynb` or `notebooks/training_models.ipynb` to generate custom model data and train a new wake word.

The automated training path is useful for:

- generating synthetic spoken examples of your target phrase
- augmenting the dataset with room noise and reverberation
- training a model with a config-driven pipeline

### 3. Evaluate the result

After training, use the model in inference mode and compare the detection score against your threshold settings.

## Environment Setup

This project is built around a Python environment with the libraries required for audio processing, model training, and OpenWakeWord inference.

### Create a virtual environment

```bash
python3 -m venv myenv
source myenv/bin/activate
```

### Install dependencies

```bash
pip install -r requirements.txt
```

### Optional: install OpenWakeWord from source

The repo already includes a local OpenWakeWord source tree under `notebooks/openwakeword`, and the environment requirements reference the project installation directly.

## Training and Inference Notes

### Inference example

The project includes a microphone-based detection loop that reads audio chunks, runs inference, and prints live scores for a wake word model.

Typical workflow:

- select a model file such as `.onnx`
- load it with `openwakeword.Model(...)`
- read frames from a microphone stream
- compute the score for each chunk
- trigger an action when the score passes a threshold

### Typical thresholding logic

```python
THRESHOLD = 0.9
COOLDOWN = 5.0
last_detection = 0.0
```

This pattern is used to avoid repeated triggers while the wake word remains active.

## Key Notebooks

- `notebooks/Train_Your_First_Wake_Word_Model.ipynb`  
  Quick validation and microphone testing for a custom or pretrained model.

- `notebooks/automatic_model_training.ipynb`  
  Full automated training pipeline for synthetic data, augmentation, and model export.

- `notebooks/training_models.ipynb`  
  More detailed manual custom-model training workflow.

- `notebooks/performance_metrics.ipynb`  
  Evaluation and scoring for validating trained models.

## Example Data Sources

The project pulls or generates data from a number of sources, including:

- AudioSet
- FMA dataset
- MIT room impulse responses
- synthetic TTS-generated wake-word examples
- validation feature arrays for false-positive estimation

## Model Outputs

Trained models and generated artifacts are typically saved into directories such as:

- `notebooks/my_custom_model/`
- `notebooks/models/`
- `notebooks/saved_model/`
- `notebooks/piper_models/`
- `trained_models/`

These outputs may include audio clips, feature arrays, ONNX models, and other intermediate artifacts.

## Notes

- This project is intended for experimentation and learning.
- Some training tasks are computationally heavy and may require a machine with GPU support.
- Audio processing and synthetic dataset generation can be time-consuming, especially for full-scale training runs.
- Model thresholds should be tuned to your target environment and microphone conditions.

## License

This project is for research and personal experimentation. Please check the upstream licenses of the libraries and datasets used when using the repository for production or public deployment.

## Acknowledgments

This project builds on the OpenWakeWord ecosystem and the broader audio ML tooling stack, including:

- OpenWakeWord
- PyTorch and ONNX tooling
- Piper TTS and synthetic speech generation
- Hugging Face datasets and model hosting

## Next Steps

Possible extensions for this project include:

- deploying the trained model in a local assistant or home automation system
- optimizing wake-word thresholds for real-world conditions
- testing multiple wake phrases and detection sensitivities
- automating retraining with custom datasets

If you want to go further, start by opening the beginner notebook and testing a local model before moving into the full training notebooks.
