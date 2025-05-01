# Fine-tuning Data Curation for LLM-based Question-Answering Using LoRA/QLoRA for a Specific Domain

This repo contains the INFO 621 final project of Our (Pineapple Programmers) team, which includes three team members: Xiaoqin Fu, Subhrajeet Ghosh, and Usama Ahmed. In this work, we propose a fine-tuning data curation method for answering questions of a specific domain: building energy.

## Install Requirements
  Python
  A conda environment for Jupyter Notebook  
  GPUs  
  Libraries according to requirements.txt
  OpenAI API key
  
## Data Preparation (Part 1)

### Step 1.1: Parsing the PDF document (raw data)
Locally perform notebooks/exploratory/PDFToTxt.ipynb to parse the PDF document "data/raw/EngineeringReference.pdf" to generate the parsed (unstructured) text file "data/processed/EngineeringReference.txt". 
 
### Step 1.2: Improving the text
Upload the unstructured text file "data/processed/EngineeringReference.txt" to your Google Drive.
Upload notebooks/exploratory/GPT4ImproveTxt.ipynb to your google colab.
On your google colab, perform GPT4ImproveTxt.ipynb to improve the parsed (unstructured) text file "EngineeringReference.txt" to generated the improved (structured) text file "data/processed/EngineeringReference1_5.txt".

### Step 1.3: Geneating fine-tuning training data
Upload notebooks/exploratory/GPT4TxtToQA.ipynb to your google colab.
On your google colab, perform GPT4ImproveTxt.ipynb to generate many (193) question-answer pairs and to save them in the text file "EngineeringReference1_5_QAGPT4.txt".
From your google colab, download the text file "EngineeringReference1_5_QAGPT4.txt" to a local folder, such as data/processed/.
Locally perform TxtToJSON.py to transfer the improve text file "EngineeringReference1_5_QAGPT4.txt" to the JSON file "EngineeringReference1_5_QAGPT4.json", as the training data.

### Step 1.4: Geneating fine-tuning testing data
Upload notebooks/exploratory/GPT4TxtToQA_testdata.ipynb to your google colab.
On your google colab, perform GPT4ImproveTxt.ipynb to generate a few (17) and different question-answer pairs and to save them in the text file "EngineeringReference1_5_TESTQAGPT4omini.txt".
From your google colab, download the text file "EngineeringReference1_5_TESTQAGPT4omini.txt" to a local folder, such as data/processed/.
Locally perform TxtToJSON.py to transfer the improve text file "EngineeringReference1_5_TESTQAGPT4omini.txt" to the JSON file "EngineeringReference1_5_TESTQAGPT4omini.json", as the testing data.

## LLM Execution (Part 2)

### Step 2.1: Fine-tuning

#### Step 2.1.1: Fine-tuning LlaMA 3.2 1B
#### Step 2.1.2: Fine-tuning LlaMA 3.2 3B

### Step 2.2: Testing

### Step 2.3: Evaluation

### Step 2.4: Statistics and analysis
