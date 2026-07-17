# Brain MRI Tumor Segmentation with DeepLabV3+

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BensuVarol/brain-mri-tumor-segmentation-deeplabv3plus/blob/main/notebooks/Brain_MRI_Tumor_Segmentation_DeepLabV3Plus_V2.ipynb)
DeepLabV3+ implementation for pixel-level brain tumor segmentation on MRI slices using an ImageNet-pretrained MobileNetV2 encoder.

## Project Overview

Brain tumor segmentation identifies tumor regions at the pixel level rather than assigning a single class to an entire MRI image. This project implements a reproducible medical image segmentation workflow that includes patient-level data splitting, transfer learning, threshold selection, detailed evaluation, and qualitative prediction visualization.

The notebook is designed for Google Colab and downloads the dataset automatically with KaggleHub.

## Dataset

The project uses the [LGG MRI Segmentation dataset](https://www.kaggle.com/datasets/mateuszbuda/lgg-mri-segmentation). It contains brain MRI slices and corresponding binary tumor masks from 110 patients.

The dataset version used during development contains:

- 3,929 unique image-mask pairs
- 1,373 tumor-positive slices
- 2,556 tumor-free slices

Raw dataset files are not stored in this repository. The notebook downloads them at runtime.

## Methodology

The workflow includes:

- Automatic dataset download with KaggleHub
- Duplicate-safe image-mask pairing
- Patient-level train, validation, and test splitting
- Stratification by patient tumor status
- MobileNetV2-compatible image preprocessing
- Training-time image augmentation
- DeepLabV3+ with an ASPP module and MobileNetV2 encoder
- Decoder warm-up followed by encoder fine-tuning
- Combined binary cross-entropy and Dice loss
- Validation-only threshold selection
- One-time final test evaluation
- Prediction-mask and overlay visualization

Patient-level splitting prevents slices belonging to the same patient from appearing in multiple subsets and reduces data leakage risk.

## Model Architecture

The model combines:

- MobileNetV2 encoder initialized with ImageNet weights
- Low-level spatial features from the encoder
- Atrous Spatial Pyramid Pooling with multiple dilation rates
- DeepLabV3+ decoder for spatial reconstruction
- Single-channel sigmoid output for binary segmentation

Training is performed in two stages:

1. Decoder warm-up while the encoder remains frozen
2. Fine-tuning of the final encoder layers with a lower learning rate

## Evaluation

The project reports:

- Global Dice score
- Global Intersection over Union
- Mean per-image Dice and IoU
- Tumor-positive image Dice and IoU
- Precision
- Recall / sensitivity
- Specificity
- Pixel accuracy
- False-positive rate on tumor-free slices

Pixel accuracy is not interpreted alone because background pixels strongly outnumber tumor pixels.

The prediction threshold is selected using only the validation set. The test set is evaluated once after the threshold has been fixed.

## Results

The cleaned notebook contains the complete evaluation pipeline. Final values are generated after running all cells in Colab and are saved to `test_metrics.csv` and `results_summary.json`.

The following files should be copied from the Colab runtime into the `results/` directory after training:

- `training_curves.png`
- `prediction_results.png`
- `validation_threshold_results.csv`
- `test_metrics.csv`
- `dataset_split_summary.csv`
- `results_summary.json`

Large model checkpoints are excluded from GitHub by `.gitignore`.

## Repository Structure

```text
brain-mri-tumor-segmentation-deeplabv3plus/
├── notebooks/
│   └── Brain_MRI_Tumor_Segmentation_DeepLabV3Plus_V2.ipynb
├── data/
│   └── README.md
├── results/
│   └── README.md
├── .gitattributes
├── .gitignore
├── README.md
└── requirements.txt
```

## How to Run

1. Open the notebook using the Colab badge above.
2. Select **Runtime > Change runtime type > GPU**.
3. Run all notebook cells in order.
4. Allow KaggleHub to download the dataset.
5. Review the selected validation threshold and final test metrics.
6. Download the generated result files if they will be added to the repository.

For local execution:

```bash
pip install -r requirements.txt
```

## Technologies Used

- Python
- TensorFlow / Keras
- OpenCV
- NumPy
- Pandas
- Matplotlib
- Scikit-learn
- KaggleHub
- Google Colab

## Limitations

- The dataset contains 2D MRI slices rather than complete 3D volumes.
- The workflow has not been externally clinically validated.
- Performance may vary across scanners, acquisition protocols, and patient populations.
- The model is intended for research and educational use only.

## Author

**Bensu Varol**  
MSc Computer Engineering Student  
Software Support Assistant Specialist  

Research interests: Medical Image Analysis, Deep Learning, Computer Vision, Explainable AI, and Healthcare AI.

## Disclaimer

This project is intended for educational and research purposes. It is not a medical device and must not be used for clinical diagnosis or treatment decisions.
