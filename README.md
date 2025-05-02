# Fine-tuning Data Curation for LLM-based Question-Answering Using LoRA/QLoRA for a Specific Domain

This repo contains the INFO 621 final project of Our (Pineapple Programmers) team, which includes three team members: Xiaoqin Fu, Subhrajeet Ghosh, and Usama Ahmed. In this work, we propose a fine-tuning data curation method for answering questions of a specific domain: building energy.

## Install Requirements
  * Python
  
  * A conda environment for Jupyter Notebook  
  
  * GPUs  
  
  * Libraries according to requirements.txt
  
  * OpenAI API key
  
## Data Preparation (Part 1)

### Step 1.1: Parsing the PDF document (raw data)

- Locally perform notebooks/exploratory/PDFToTxt.ipynb to parse the PDF document "data/raw/EngineeringReference.pdf" to generate the parsed (unstructured) text file "data/processed/EngineeringReference.txt". 
 
### Step 1.2: Improving the text

- Upload the unstructured text file "data/processed/EngineeringReference.txt" to your Google Drive.

- Upload notebooks/exploratory/GPT4ImproveTxt.ipynb to your google colab.

- On your google colab, perform GPT4ImproveTxt.ipynb to improve the parsed (unstructured) text file "EngineeringReference.txt" to generated the improved (structured) text file "data/processed/EngineeringReference1_5.txt".

### Step 1.3: Geneating fine-tuning training data

- Upload notebooks/exploratory/GPT4TxtToQA.ipynb to your google colab.

- On your google colab, perform GPT4ImproveTxt.ipynb to generate many (193) question-answer pairs and to save them in the text file "EngineeringReference1_5_QAGPT4.txt".

- From your google colab, download the text file "EngineeringReference1_5_QAGPT4.txt" to a local folder, such as data/processed/.

- Locally perform TxtToJSON.py to transfer the improve text file "EngineeringReference1_5_QAGPT4.txt" to the JSON file "EngineeringReference1_5_QAGPT4.json", as the training data.

### Step 1.4: Geneating fine-tuning testing data

- Upload notebooks/exploratory/GPT4TxtToQA_testdata.ipynb to your google colab.

- On your google colab, perform GPT4ImproveTxt.ipynb to generate a few (17) and different question-answer pairs and to save them in the text file "EngineeringReference1_5_TESTQAGPT4omini.txt".

- From your google colab, download the text file "EngineeringReference1_5_TESTQAGPT4omini.txt" to a local folder, such as data/processed/.

- Locally perform TxtToJSON.py to transfer the improve text file "EngineeringReference1_5_TESTQAGPT4omini.txt" to the JSON file "EngineeringReference1_5_TESTQAGPT4omini.json", as the testing data.

## LLM Execution (Part 2)

/srv/data1/fuxiaoqin/

### Step 2.1: Fine-tuning and Testing 

- Upload the traning data “EngineeringReference1_5_QAGPT4.json“ and the testing data "EngineeringReference1_5_TESTQAGPT4omini.json" to a folder (such as /srv/data1/fuxiaoqin/Downloads/) in the server with a conda environment and (three 80 GB NVIDIA H100) GPUs.

#### Step 2.1.1: Fine-tuning and Testing LlaMA 3.2 1B

- Upload LoRAQLoRA_FinetuneLlama_1B.ipynb to the server.

- Perform LoRAQLoRA_FinetuneLlama_1B.ipynb.

- Upload generated metric files (i.e., Metrics_LM32_1B_Before.csv, Metrics_LM32_1B_QA_LoRA.csv, Metrics_LM32_1B_QA_QLoRA.csv) and result files ((i.e., Results_LM32_1B_Before.csv, Results_LM32_1B_QA_LoRA.csv, Results_LM32_1B_QA_QLoRA.csv)) from the server to your google colab.
(Note: *_Before.csv files mean for the foundation model (base) before the fine-tuning.)

#### Step 2.1.2: Fine-tuning and Testing LlaMA 3.2 3B

- Upload LoRAQLoRA_FinetuneLlama_3B.ipynb to the server.

- Perform LoRAQLoRA_FinetuneLlama_3B.ipynb.

- Upload generated metric files (i.e., Metrics_LM32_3B_Before.csv, Metrics_LM32_3B_QA_LoRA.csv, Metrics_LM32_3B_QA_QLoRA.csv) and result files ((i.e., Results_LM32_3B_Before.csv, Results_LM32_3B_QA_LoRA.csv, Results_LM32_3B_QA_QLoRA.csv)) from the server to your google colab.
(Note: *_Before.csv files mean for the foundation model (base) before the fine-tuning.)

### Step 2.2: Evaluation

- Upload the evaluation program notebooks/exploratory/GPT4GradeQAs.ipynb to your google colab.

#### Step 2.2.1: Evaluating LlaMA 3.2 1B Results

- In notebooks/exploratory/GPT4GradeQAs.ipynb, find two lines:
  + csvFile = pandas.read_csv('/content/drive/MyDrive/Results_LM32_1B_Before.csv', sep=',', header=0, encoding='utf-8')
  + output_name = "Results_LM32_1B_Before_Scores_"+str(times+1)+".csv"
- Update the file path and name (Results_LM32_1B_Before) to your 

#### Step 2.2.2: Evaluating LlaMA 3.2 3B Results

### Step 2.3: Statistics and analysis
