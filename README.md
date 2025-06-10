# InciTagger

I built `InciTagger`, a custom **Named Entity Recognition (NER)** model that automatically extracts structured information such as incident ID, date, time, location, incident type, and root cause from unstructured accident reports. 

This helps in efficiently analyzing and managing safety data by turning free-form text into actionable insights.

## 💡 Motivation

Accident reports hold vital safety information but are often written in unstructured, free-form text. 

This makes it difficult to automatically extract and analyze key insights like incident types, locations, and root causes. 

I built `InciTagger` to solve this problem by using Named Entity Recognition (NER) to convert unstructured reports into structured data. 

This enables faster, more reliable safety analysis and helps organizations make informed decisions.

## 🧠 Features

- Named Entity Recognition for:
  - `INCIDENT_ID`, `DATE`, `TIME`
  - `SITE`, `REGION`, `INCIDENT_TYPE`
  - `SEVERITY_LEVEL`, `PROCEDURE_CODE`
  - `ROOT_CAUSE_DESC`, `ROOT_CAUSE_CATEGORY`, `PREVENTION_RECOMMEND`
- Built and trained with spaCy
- Training data prepared from structured JSON using custom preprocessing
- Easy prediction and evaluation on custom sentences

## 🚀 Quick Start

Follow the steps below to set up and run **ClassiCancer** on your local machine:

### 1. Clone the Repository

```bash
git clone git@github.com:MDAAMIRAHMED/InciTagger.git
cd InciTagger
```

### 2. Open the project notebook in Google Colab 
   You can run all steps including data preprocessing, model training, and evaluation directly in Colab.
   
### 3. Upload the dataset (.json file) and base_config.cfg to Colab
Download the dataset from the following link and place it in the project root folder:

📦 [Download Dataset](https://huggingface.co/datasets/MongoDB/accident_reports/blob/main/accidents_reports.json)

### 4. Complete Training & Loading Workflow

```bash
# Step 1: Generate a complete config file from base_config
!python -m spacy init fill-config base_config.cfg config.cfg

# Step 2: Train the model using the filled config
!python -m spacy train config.cfg --output ./output --paths.train ./train.spacy --paths.dev ./dev.spacy

# Step 3: Load the trained model
import spacy
ner_model = spacy.load("output/model-best")

# Step 4: Test the model with a sample input
text = "On March 08, 2024 at 09:01, a Equipment Failure occurred at Factory B in the East region. The incident ID is INC-2024-001."
doc = ner_model(text)

for ent in doc.ents:
    print(ent.text, "->", ent.label_)
```

## 🤝 Contributing

This project is currently maintained by me. Feel free to open issues or suggest improvements.
