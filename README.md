# RomanSetu
Romansetu addresses the challenge of extending Large Language Models (LLMs) to non-English languages using non-Latin scripts. We propose an approach that harnesses the power of romanized text as an interface for LLMs, leveraging its frequent informal use and shared tokens with English to enhance cross-lingual alignment.
## Contents
- [Abstract](#Abstract)
- [Instructions](#Instructions)
- [Models](#Models)
- [Data](#Data)
- [Scripts](#Scripts)

## Abstract
This study presents an approach that involves the continual pretraining of an English LLM, such as Llama 2, on romanized text of non-English, non-Roman script languages, followed by instruction tuning on romanized data. The results demonstrate that romanized text not only reduces token fertility by 2x-4x but also matches or surpasses native script representation across various Natural Language Understanding (NLU), Natural Language Generation (NLG), and Machine Translation (MT) tasks. Furthermore, embeddings computed on romanized text exhibit closer alignment with their English translations than those from the native script. This approach offers a promising direction for leveraging the capabilities of English LLMs in languages traditionally underrepresented in Natural Language Processing (NLP).

This repository contains all the resources necessary for replicating the experiments and findings reported in the paper. You will find detailed instructions for training and evaluations, along with the provided models, datasets, scripts, and other relevant materials.
## Instructions

## Models
All our models are hosted on Hugging Face and can be easily loaded using the 🤗 Transformers library.
```py
from transformers import AutoTokenizer, AutoModelForCausalLM

model_path = "model/path/here" # Eg. "ai4bharat/romansetu-cpt-roman-200m"

tokenizer = AutoTokenizer.from_pretrained(model_path)
model = AutoModelForCausalLM.from_pretrained(model_path)
```


### Continual Pre-Trained (CPT) models
| Model           | 100m         | 200m         | 300m         | 400m         | 500m         |
|-----------------|--------------|--------------|--------------|--------------|--------------|
| CPT - Native    | [link](https://huggingface.co/ai4bharat/romansetu-cpt-native-100m) | [link](https://huggingface.co/ai4bharat/romansetu-cpt-native-200m) | [link](https://huggingface.co/ai4bharat/romansetu-cpt-native-300m) | [link](https://huggingface.co/ai4bharat/romansetu-cpt-native-400m) | [link](https://huggingface.co/ai4bharat/romansetu-cpt-native-500m) |
| CPT - Romanized | [link](https://huggingface.co/ai4bharat/romansetu-cpt-roman-100m) | [link](https://huggingface.co/ai4bharat/romansetu-cpt-roman-200m) | [link](https://huggingface.co/ai4bharat/romansetu-cpt-roman-300m) | [link](https://huggingface.co/ai4bharat/romansetu-cpt-roman-400m) | [link](https://huggingface.co/ai4bharat/romansetu-cpt-roman-500m) |

### Instruction Fine-Tuned models
| Model           | Native       | Romanized    |
|-----------------|--------------|--------------|
| BaseLLM         | [link](https://huggingface.co/ai4bharat/romansetu-base-sft-native) | [link](https://huggingface.co/ai4bharat/romansetu-base-sft-roman) |
| CPT - Native    | [link](https://huggingface.co/ai4bharat/romansetu-cpt-native-sft-native) |      -       |
| CPT - Romanized |      -       | [link](https://huggingface.co/ai4bharat/romansetu-cpt-roman-sft-roman) |
## Data

### Training
#### Continual Pre-training data
For continual pretraining, we sourced approximately 500 million words of document-level data from web-crawled corpora for each language under consideration along with English. To generate the romanized dataset, we transliterated the native script dataset using the IndicXlit model, a state-of-the-art open-source transliteration model for Indian languages. Both the native script dataset and its romanized counterpart were then used for continual pretraining in various configurations explained later.

#### Instruction fine-tuning data
These languages have very little native instruction tuning data for diverse tasks. We rely on translating high-quality English-supervised instruction-tuning datasets into the languages under consideration. We use IndicTrans2, the state-of-the-art open-source MT model for Indian languages compared to commercial offerings for translation. We sampled examples from various English instruction tuning datasets to ensure a diverse mix of tasks from the Flan collection (65k) and Dolly (15k) and 20k high-quality manually translated examples in each direction from the BPCC-Human subset. Thus, the final IFT dataset has 120k examples per language. The instruction tuning datasets are further romanized using IndicXlit.

### Evaluation
For evaluation, we use the following benchmarks, including their romanized variants for comparison.

#### Machine Translation
* FLORES-200 devtest
* IN22 test set
#### Natural Language Generation (NLG) Tasks 
* IndicNLG Suite benchmarks (Summarization and Headline Generation)
#### Natural Language Understanding (NLU) Tasks
* IndicXTREME (IndicSentiment, IndicXNLI, IndicCOPA, IndicQA)
#### Reasoning tasks
* Translate NLU tasks (MMLU, Hellaswag, BoolQ, ARC, Commonsense-QA)
