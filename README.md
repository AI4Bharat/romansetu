# RomanSetu
Romansetu addresses the challenge of extending Large Language Models (LLMs) to non-English languages using non-Latin scripts. We propose an approach that harnesses the power of romanized text as an interface for LLMs, leveraging its frequent informal use and shared tokens with English to enhance cross-lingual alignment.
## contents
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

### Continualy Pre - trained (CPT) models
| Model           | 100m         | 200m         | 300m         | 400m         | 500m         |
|-----------------|--------------|--------------|--------------|--------------|--------------|
| CPT - Native    | [download]() | [download]() | [download]() | [download]() | [download]() |
| CPT - Romanized | [download]() | [download]() | [download]() | [download]() | [download]() |

### Instruction fine-tuned models
| Model           | Native       | Romanized    |
|-----------------|--------------|--------------|
| BaseLLM         | [download]() | [download]() |
| CPT - Native    | [download]() |      -       |
| CPT - Romanized |      -       | [download]() |
## Datas

### Training

### Evaluation
## Scripts
