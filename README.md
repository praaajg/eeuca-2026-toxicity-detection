# LINUS@EEUCA 2026: Fine-grained Toxicity Detection in Gaming Chat using Multilingual Transformers

This repository contains the official code for the paper **"LINUS@EEUCA 2026: Fine-grained Toxicity Detection in Gaming Chat using Multilingual Transformers"**, accepted at the 9th Workshop on Event Extraction and Understanding: Challenges and Applications (EEUCA 2026).

**Paper:** [https://aclanthology.org/2026.eeuca-1.24v2.pdf](https://aclanthology.org/2026.eeuca-1.24v2.pdf)

**Authors:** Prajwal Ghimire, Aashish Mahato, Sunil Regmi

**Abstract:** The detection of toxic behavior in online gaming communities is crucial for maintaining safe digital spaces, yet remains challenging due to subtle context dependent and intent driven language. The GameTox dataset consists of around 53K World of Tanks chat utterances annotated across six categories: Non-toxic, Insults and Flaming, Other Offensive Texts, Hate and Harassment, Threats, and Extremism. We compare five multilingual transformer encoders for this task. The mmBERT-base fine-tuned with class weighted cross-entropy loss achieved the strongest validation performance among the evaluated models with a Macro F1 score of 0.5882. Our final system resulted in official test Macro F1 of 0.5104 on the shared task leaderboard. An additional evaluation on an internal held out development portion yielded a Macro F1 of 0.4282, indicating substantial variation across evaluation splits. We further discuss the challenges associated with the extremely rare Threats and Extremism categories and discuss the limitations of class weighted training when only a small number of minority class examples are available.


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
    editor = {H{\"u}rriyeto{\u{g}}lu, Ali  and
      Thapa, Surendrabikram  and
      Tanev, Hristo  and
      Adhikari, Surabhi},
    booktitle = "Proceedings of the 9th Workshop on Event Extraction and Understanding: Challenges and Applications ({EEUCA} 2026)",
    month = jul,
    year = "2026",
    address = "San Diego, California, USA",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2026.eeuca-1.24v2.pdf",
    doi = "10.18653/v2/2026.eeuca-1.24",
    pages = "216--222",
    ISBN = "979-8-89176-402-6",
    abstract = "The detection of toxic behavior in online gaming communities is crucial for maintaining safe digital spaces, yet remains challenging due to subtle context-dependent and intent-driven language. The GameTox dataset consists of around 53K World of Tanks chat utterances annotated across six categories: Non-toxic, Insults and Flaming, Other Offensive Texts, Hate and Harassment, Threats, and Extremism (CITATION). Our best performing approach, across multiple transformer-based architecture experimentations, is based on the multilingual BERT variant mmBERT-base fine-tuned with class-weighted cross-entropy loss. The best mmBERT-base model achieved a Macro F1 of 0.5882 during validation and an official test Macro F1 of 0.5104 on the shared task leaderboard. An internal held-out evaluation on a development split yielded 0.4282, which we analyze to understand distributional sensitivity to gaming slang and class imbalance. The code is available at: \url{https://github.com/sunilRegmi-ai/eeuca-toxicity-detection}."
}

```
