# DVERGE Fine-tuning Guide

This repository contains modifications and fine-tuning implementations of DVERGE (Diversifying Vulnerabilities for Enhanced Robust Generation of Ensembles) for ongoing research.

## Dependencies

Create a Conda environment named `dverge` with all dependencies by running:

```sh
conda env create -f environment.yml
```

We use **PyTorch 1.4.0**, but you may need to adjust the PyTorch version according to the CUDA version on your machine.

The code is tested on a **single TITAN Xp GPU**. Running on multiple GPUs may require modifications.

## Data and Pre-trained Models

Access the pre-trained models and black-box transfer adversarial examples via [this link](https://drive.google.com/drive/folders/1i96Bk_bCWXhb7afSNp1t3woNjO1kAMDH?usp=sharing).

1. Download and place the **`checkpoints/`** folder under this repository.
2. Create a folder named **`data/`**, download **`transfer_adv_examples.zip`**, unzip it, and place the extracted **`transfer_adv_examples/`** folder inside `data/`.

## Fine-tuning DVERGE

### Training
Modify and execute the training script for fine-tuning:

```sh
bash scripts/training.sh
```

### Evaluation
Run the evaluation script to test the model:

```sh
bash scripts/evaluation.sh
```

### Feature Extraction Adjustments
The current feature extraction method mainly supports **ResNet20**. If using a different architecture, modify the feature extraction mechanism using **PyTorch forward hooks**.

### Stability Considerations
Training DVERGE may result in high variations due to **random layer sampling** for distillation. See **Appendix C.5** of the paper for more details.

## Decision Region Visualization
To understand decision region plots, refer to [this tutorial](https://adversarial-ml-tutorial.org/adversarial_training/).

Our code for decision region visualization can be found [here](https://drive.google.com/file/d/1KNoQGTXm3g_RBwE0a6IkrlSks4Wez_tN/view). Key settings:

- `args.steps=1000`: Each axis perturbed **1000 times**.
- `args.vmax=0.1`: Maximum perturbation distance **0.1**.
- Generates **1,000,000 data points** per plot.

## Citation
If you use this work, please cite:

```bibtex
@article{yang2020dverge,
  title={DVERGE: Diversifying Vulnerabilities for Enhanced Robust Generation of Ensembles},
  author={Yang, Huanrui and Zhang, Jingyang and Dong, Hongliang and Inkawhich, Nathan and Gardner, Andrew and Touchet, Andrew and Wilkes, Wesley and Berry, Heath and Li, Hai},
  journal={Advances in Neural Information Processing Systems},
  volume={33},
  year={2020}
}
```

## Acknowledgment
This repository adapts the **Adaptive Diversity Promoting Regularizer (ADP)** training code from its [official repo](https://github.com/P2333/Adaptive-Diversity-Promoting), originally in TensorFlow, and converted into PyTorch here.


