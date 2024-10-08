# Working Project :Large Language Models for Education

## Table of Contents
- [Introduction](#introduction)
- [Problems Addressed](#problems-addressed)
- [Research Questions](#research-questions)
- [Datasets Overview](#datasets-overview)
- [Project Structure](#project-structure)
- [Setup and reqruirements](#Setup and reqruirements)
- [LLMs Code for Fairness and Bias Reduction](#llms-code-for-fairness-and-bias-reduction)
  - [1. Fine-Tuning GPT-3](#1-fine-tuning-gpt-3)
  - [2. Bias Mitigation using BART](#2-bias-mitigation-using-bart)
  - [3. Analyzing Bias in Datasets](#3-analyzing-bias-in-datasets)
- [Conclusion](#conclusion)
- [Requirements](#requirements)

## Introduction
Large Language Models (LLMs) have emerged as transformative tools in various domains, particularly in education. These models, such as GPT-3 and BART, have the potential to enhance learning experiences, provide personalized educational content, and facilitate communication between students and educational systems. However, the deployment of LLMs also raises significant concerns regarding fairness, especially for underrepresented groups. This project aims to explore these challenges and develop solutions that ensure equitable outcomes in AI-driven learning environments.

## Problems Addressing
The project focuses on several critical issues:

- **Bias in Training Datasets**: Many LLMs are trained on datasets that may not adequately represent diverse populations, leading to biased outputs that can negatively affect marginalized students.
- **Impact of Missing Data**: The absence of data representing underrepresented groups can result in a lack of relevant educational resources and support.
- **Inaccurate Data Representation**: Misrepresentation of certain groups in training data can perpetuate stereotypes and hinder the effectiveness of educational tools.
- **Balancing Fairness with Performance**: Striking a balance between achieving high performance in language tasks while maintaining fairness is a complex challenge.

## Research Questions
To guide this project, the following research questions have been formulated:

1. How can we identify and mitigate biases present in existing LLMs used for educational purposes?
2. What methods can be employed to ensure that training datasets are representative of diverse student populations?
3. How does the missing representation of certain groups impact the effectiveness of LLMs in educational settings?
4. What strategies can be implemented to balance fairness and performance in AI-driven educational tools?

## Datasets Overview
The success of this project relies on utilizing diverse datasets that reflect the varied backgrounds of students. Key datasets include:

- **Common Crawl**: A vast dataset containing web pages from across the internet, which can be filtered for diversity.
- **OpenAI's GPT-3 Dataset**: Includes a wide range of text but requires careful curation to address bias.
- **Custom Educational Datasets**: Datasets specifically designed to include voices from underrepresented groups in education.

These datasets will be analyzed for bias and representation, ensuring that the models trained on them are more equitable.

## Initial Project Structure
```bash
│
├── data/
│ ├── training_data.jsonl # Custom training dataset
│ ├── common_crawl_data.json # Filtered Common Crawl dataset
│ └── bias_analysis_results.csv # Results from bias analysis
│
├── src/
│ ├── fine_tune_gpt3.py # Script for fine-tuning GPT-3
│ ├── mitigate_bias_bart.py # Script for bias mitigation using BART
│ └── analyze_bias.py # Script for analyzing bias in datasets
│
├── models/
│ ├── gpt3_model_finetuned.pth # Fine-tuned GPT-3 model
│ └── bart_model_finetuned.pth # Fine-tuned BART model
│
├── requirements.txt # Required Python packages
└── README.md
```
## Setup and reqruirements
Clone the Repository:
``` 
git clone https://github.com/Arif5533/Fairness-in-LLMs.git
cd Fairness-in-LLMs
```
Create a Virtual Environment (recommended):
```
python -m venv venv      # Create a virtual environment named 'venv'
source venv/bin/activate # Activate the virtual environment (Linux/Mac)
.\venv\Scripts\activate  # Activate the virtual environment (Windows)
```
Install Requirements:
To install all necessary Python packages listed in requirements.txt, run:
```
pip install -r requirements.txt
```

## LLMs Code for Fairness and Bias Reduction

### 1. Fine-Tuning GPT-3

#### File: `src/fine_tune_gpt3.py`
```
import openai
import json

# Initialize OpenAI API
openai.api_key = 'YOUR_API_KEY'

# Load custom training data
def load_training_data(file_path):
    with open(file_path, 'r') as f:
        return json.load(f)

training_data = load_training_data('data/training_data.jsonl')

# Fine-tuning parameters
fine_tune_params = {
    "model": "davinci",
    "training_data": training_data,
    "n_epochs": 4,
    "learning_rate_multiplier": 0.1,
}

# Fine-tune model
response = openai.FineTune.create(**fine_tune_params)
print("Fine-tuning response:", response)
```
###Bias Mitigation using BART
#### File: src/mitigate_bias_bart.py

```
from transformers import BartForConditionalGeneration, BartTokenizer

# Load pre-trained BART model and tokenizer
model = BartForConditionalGeneration.from_pretrained('facebook/bart-large')
tokenizer = BartTokenizer.from_pretrained('facebook/bart-large')

# Define input text with potential biases
input_text = "Your biased input text here."

# Tokenize input text
inputs = tokenizer(input_text, return_tensors="pt")

# Generate output with bias mitigation techniques applied
outputs = model.generate(**inputs)
output_text = tokenizer.decode(outputs, skip_special_tokens=True)

print("Output after bias mitigation:", output_text)
```


