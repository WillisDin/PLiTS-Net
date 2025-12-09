# PLiTS-Net Repository (Ongoing)

**NOTE: This repository provides datasets and reference implementations for the PLiTS-Net framework. The content is continuously updated. If you have any questions, please contact the corresponding author of the paper.**

---

## 1. Datasets

- **`WeiboDRP_MLCS.zip`**
  - Includes the original **WeiboDRP_MLCS** dataset.
  - Also includes a re-parsed version that matches the data format used by the **PLiTS-Net** architecture, provided for reproducibility and reference.

- **Weibo-2025 DataSet**
  - Contains the raw, unparsed original dataset.

- **Other datasets**
  - All remaining datasets used in the paper are publicly available.
  - Please refer to the paper for the corresponding sources and download links.

---

## 2. Default Hyperparameters (for Efficiency Comparison)

For fair and efficient comparison, all model implementations in this repository use the following default settings:

- Learning rate: **0.0003**
- Batch size: **32**
- Epochs: **10**
- Dropout: **0.3**
- Max sequence length: **256**

Notes:
- The code is provided as a reference implementation. When reproducing experiments, you may need to modify variable names, file paths, and dataset parsing logic to match your local setup.
- Due to differences in datasets, tasks, and data parsing procedures, reproduction may produce small performance fluctuations compared with the paper. However, the overall trends and conclusions should remain consistent.

---

## 3. PLiTS-Net Model Code (Full Reference Version)

The PLiTS-Net code in this repository is provided as a **full reference implementation**. The core idea is:

- After fully fine-tuning the PLM on a smaller dataset, the PLiTS-Net design can achieve **stronger transferability** and **better performance** on related tasks/datasets **while keeping the PLM frozen**, outperforming alternative architectures.

Hardware note:
- This full reference version can be **GPU memory intensive**, because it includes a component that fully fine-tunes the PLM on small data and may require parallel computation at the scale of:
  - **Batch Size × Max Length × Max Turns**

Practical recommendation:
- In real usage, you can first run a PLM baseline model to fully fine-tune on a small dataset and **save the outputs/checkpoints**.
- Then load and integrate them into the PLiTS-Net pipeline for transfer training on larger datasets.
- This can significantly reduce computational cost.

---

## 4. LLM Prompts (Root vs. Non-root Nodes)

For LLM-based methods, we use two prompts to handle different cases:

### 4.1 Root Node (no parent post)

You are a linguistics expert proficient specializing in sentiment analysis of social media content. Please analyze the sentiment polarity of the following Chinese text, which is about the topic of "delayed retirement". Do Not explain, Only respond with one word: positive, negative, or neutral. 
Text:
"{text}"

### 4.2 Non-root Node (with a parent post)
You are a linguistics expert proficient specializing in sentiment analysis of social media content. The following is a reply to another post. Based on the context of both the reply and the original post, analyze the sentiment polarity of the reply regarding the topic of "delayed retirement". Do Not explain, Only respond with one word: positive, negative, or neutral. 
Reply:
"{text}"
Original Post:
"{parent_text}"

---

