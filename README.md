# Aya-Indic-Qwen3-4B

This project fine-tunes **Qwen3-4B-Instruct** on the **Indic subset of the Aya dataset** using [Unsloth](https://github.com/unslothai/unsloth).  
The goal is to improve **instruction-following and conversational abilities** of the model in Indian languages such as Hindi, Bengali, Tamil, Telugu, and others.

---

## 📌 Overview

- **Base Model**: Qwen3-4B-Instruct  
- **Dataset**: CohereLabs/Aya dataset (filtered to Indian languages only)  
- **Finetuning Type**: Parameter-efficient fine-tuning with LoRA  
- **Frameworks**: Unsloth + Hugging Face TRL  
- **Objective**: Create a compact multilingual assistant focused on Indian languages.  

---

## 🔄 Process

### 1. Dataset Preparation
- Start with the **Aya dataset**, which contains multilingual instruction–response pairs.  
- Select only the **Indic languages** (Hindi, Bengali, Tamil, Telugu, Marathi, Gujarati, Kannada, Malayalam, Punjabi, Sindhi, Urdu).  
- Convert examples into a **conversation-style format** with user and assistant roles.

### 2. Applying Chat Template
- Use the **Qwen3 instruction template** to structure conversations.  
- This ensures the data matches the model’s expected input/output format.  
- Each example becomes a structured dialogue (`user → assistant`).

### 3. Training Setup
- Fine-tune using **LoRA adapters** for efficiency (only a fraction of parameters are updated).  
- Training is run in **4-bit quantization** to reduce GPU memory usage.  
- Loss is computed **only on assistant responses** (not user inputs) to improve output quality.

### 4. Fine-tuning
- Run supervised fine-tuning with **SFTTrainer** from Hugging Face TRL.  
- Training includes gradient accumulation, learning rate scheduling, and mixed precision for speed and stability.  
- The model learns to better generate answers in Indic languages.

### 5. Inference & Testing
- Provide prompts in Indian languages (e.g., translations, explanations, Q&A).  
- The fine-tuned model responds using the training-aligned chat format.  
- Performance is evaluated qualitatively through test prompts.

### 6. Saving & Deployment
- Save LoRA adapters locally or push them to Hugging Face Hub.  
- Optionally merge into a **16-bit model** or convert to **GGUF** format for deployment with tools like `llama.cpp` or **Ollama**.  
