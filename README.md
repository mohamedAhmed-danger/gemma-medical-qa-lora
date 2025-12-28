# Gemma Medical QA (LoRA) 🩺

This repository contains a medical question–answering project built by fine-tuning **Google Gemma-2-2B-IT** using **LoRA (Low-Rank Adaptation)**.  
The goal is to adapt a general-purpose large language model to the **medical QA domain** in a parameter-efficient and reproducible way.

> ⚠️ This project is intended for **educational and research purposes only**.  
> It does **not** replace professional medical advice.

---

## 📌 Project Overview

- **Base Model:** `google/gemma-2-2b-it` (gated, requires Hugging Face access)
- **Fine-tuning Method:** PEFT / LoRA
- **Task:** Medical Question Answering
- **Frameworks:** PyTorch, Hugging Face Transformers, PEFT, TRL
- **Environment:** Google Colab (GPU)

The fine-tuned **LoRA adapters and tokenizer** are hosted on **Hugging Face Hub**, while this repository provides:
- the full **training & evaluation notebook**
- documentation on how to **load and test** the trained adapters

---

## 📂 Repository Contents
```
.
├── gemmaqa.ipynb # End-to-end notebook: data prep, training, evaluation, inference
└── README.md # Project documentation
```

Large artifacts such as:
- training checkpoints  
- datasets  
- model weights  

are **not included** in this repository due to size limits.

---

## 🤗 Hugging Face Model Repository

The trained LoRA adapters and tokenizer produced in this project are publicly available on Hugging Face Hub.

👉 **Hugging Face Link:**  
https://huggingface.co/azizdeniz890/gemma-medical-qa-lora

This repository contains:
- LoRA adapter weights  
- tokenizer files  
- configuration artifacts required for inference  

Using these files, the model can be loaded and tested **without re-training**, provided that access to the base model (`google/gemma-2-2b-it`) is granted.

---

## 🧠 Dataset

- **Name:** `lavita/ChatDoctor-HealthCareMagic-100k`
- **Type:** Medical instruction–question–answer pairs
- **Usage:** Reformatted into chat-style conversations compatible with Gemma

Basic preprocessing steps:
- URL and noise removal  
- whitespace normalization  
- conversion into Gemma-compatible chat templates  

---

## ⚙️ Training Summary

- **Quantization:** 4-bit (NF4, bitsandbytes)
- **Trainable Parameters:** ~0.8% (LoRA only)
- **Optimizer:** Paged AdamW
- **Sequence Length:** 512
- **Evaluation:** Step-based validation loss tracking

The training process exhibits a **stable decrease in validation loss**, indicating effective domain adaptation to medical question answering.

---

## 🔗 Trained LoRA Adapter (Hugging Face)

The final LoRA adapters and tokenizer are hosted on Hugging Face:

👉 **Model Repository:**  
https://huggingface.co/azizdeniz890/gemma-medical-qa-lora

These artifacts are sufficient to reproduce inference without repeating the training process.

---

## 🚀 How to Run Inference

1. Ensure you have access to the gated base model `google/gemma-2-2b-it`
2. Authenticate with Hugging Face:
   ```bash
   huggingface-cli login
   ```
## Load the Base Model and Attach the LoRA Adapter

The base language model is loaded in quantized form and the trained LoRA adapter is attached on top of it  
(example code for this process is provided in the notebook).

Once loaded, the model supports **chat-style medical questions** and generates **structured, professional responses**.  
Throughout inference, the model consistently emphasizes the importance of **clinical evaluation** and does not replace professional medical judgment.

---

## 📊 Results (Qualitative)

The fine-tuned model demonstrates:

- awareness of chronic conditions and potential drug interactions  
- a cautious response style with clear referral to healthcare professionals  
- coherent, context-aware, and medically grounded explanations  

Tested example domains include:
- chronic disease management  
- pediatric respiratory symptoms  
- medication safety and contraindications  

---

## 🔮 Future Work

- Training with more powerful GPUs to enable longer fine-tuning schedules  
- Quantitative evaluation using metrics such as BLEU, ROUGE, or expert clinical review  
- Fine-tuning on additional or more specialized medical datasets  
- Deployment as an interactive medical question–answering assistant  

---

## 👤 Author

**Aziz Deniz Akmermer**  
Artificial Intelligence Engineering  
Ostim Technical University  

---

## 📜 License

This project follows the license terms of the base model (**Gemma**) and the dataset used.  
Please consult the respective licenses before reuse.
