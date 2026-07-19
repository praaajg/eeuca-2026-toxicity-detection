# LINUS@EEUCA 2026: Fine-grained Toxicity Detection in Gaming Chat using Multilingual Transformers

This repository contains the official code for the paper **"LINUS@EEUCA 2026: Fine-grained Toxicity Detection in Gaming Chat using Multilingual Transformers"**, accepted at the 9th Workshop on Event Extraction and Understanding: Challenges and Applications (EEUCA 2026).

**Paper:** [https://aclanthology.org/2026.eeuca-1.24/](https://aclanthology.org/2026.eeuca-1.24/)

**Authors:** Prajwal Ghimire, Aashish Mahato, Sunil Regmi

**Abstract:** The detection of toxic behavior in online gaming communities is crucial for maintaining safe digital spaces, yet remains challenging due to subtle context-dependent and intent-driven language. The GameTox dataset consists of around 53K World of Tanks chat utterances annotated across six categories: Non-toxic, Insults and Flaming, Other Offensive Texts, Hate and Harassment, Threats, and Extremism. Our best performing approach, across multiple transformer-based architecture experimentations, is based on the multilingual BERT variant mmBERT-base fine-tuned with class-weighted cross-entropy loss.

---

## Results

| Model | Val F1 | Test F1 | Test Acc |
|-------|--------|---------|----------|
| Toxic-XLM-RoBERTa | 0.3558 | 0.3520 | 0.8281 |
| XLM-RoBERTa | 0.3830 | 0.3839 | 0.8130 |
| m-DistilBERT | 0.3907 | 0.3578 | 0.7942 |
| m-BERT | 0.4146 | 0.4243 | 0.8249 |
| **mmBERT-base** | **0.5882** | **0.5104** | **0.8716** |

### Best Hyperparameters (mmBERT-base)

| Parameter | Value |
|-----------|-------|
| Max sequence length | 32 |
| Batch size | 64 |
| Learning rate | 1e-5 |
| Weight decay | 0.01 |
| Max epochs | 10 |
| Early stopping patience | 3 |
| Loss function | Class-weighted CrossEntropyLoss |

---

## Dataset

**GameTox** — ~53,000 World of Tanks chat utterances with 6 categories:

| Label | Category |
|-------|----------|
| 0 | Non-toxic |
| 1 | Insults and Flaming |
| 2 | Other Offensive Texts |
| 3 | Hate and Harassment |
| 4 | Threats |
| 5 | Extremism |

---

## Repository Structure

```
├── multilingual_training/     # Primary training pipeline (paper results)
│   ├── train_multilingual.py  # Hugging Face Trainer-based multi-model training
│   ├── multilingual_results.csv
│   └── README.md
├── config/
│   ├── config.yaml            # Training configuration
│   └── config.json
├── data/                      # GameTox dataset splits
├── inference/
│   └── inference.py           # Inference script
├── requirements.txt           # Python dependencies
├── LICENSE                    # MIT License
└── README.md
```

---

## Usage

### Primary Pipeline (Paper Results)

```bash
cd multilingual_training
pip install -r requirements.txt
python train_multilingual.py
```

All models and hyperparameters are configured via `config/config.yaml`.

---

## Citation

```bibtex
@inproceedings{ghimire-etal-2026-linus,
    title = "{LINUS}@{EEUCA} 2026: Fine-grained Toxicity Detection in Gaming Chat using Multilingual Transformers",
    author = "Ghimire, Prajwal  and
      Mahato, Aashish  and
      Regmi, Sunil",
    booktitle = "Proceedings of the 9th Workshop on Event Extraction and Understanding: Challenges and Applications ({EEUCA} 2026)",
    month = jul,
    year = "2026",
    address = "San Diego, California, USA",
    publisher = "Association for Computational Linguistics",
    pages = "216--222",
    doi = "10.18653/v1/2026.eeuca-1.24"
}
```
