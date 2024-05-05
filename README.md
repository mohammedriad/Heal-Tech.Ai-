# Heal Tech.Ai

Heal Teach.AI, transforms the way medical information is managed by offering innovative tools to healthcare professionals like doctors and nurses. These tools are designed to improve efficiency and cut down costs. With the help of predictive text technology, data entry becomes quicker and more correct. Additionally, our summarization feature condenses patient information, giving doctors a comprehensive view of their medical history in less time. Moreover, our Medical Chatbot acts as a dependable resource for medical inquiries. All these services are powered by advanced language models trained on extensive medical data. Heal Teach.AI ensures the privacy of each registered doctor/nurse and perfects medical workflow to enhance patient care.

## Methodology 

we use Large Language Models for each service we have 
and fine tune it to be specific for its task , also each model have its specific data  

### 1- Summarization Model (FlanT5)

The FlanT5 model was chosen for its effectiveness in text summarization tasks. To enhance model efficiency, quantization was employed to reduce its size and improve inference speed. Quantization is a technique used to compress model parameters by representing them with lower precision numbers. This reduces the memory footprint of the model and enables faster computation during inference.

#### Experimentation with DialogSum Dataset (first attempt) 
Initially, the model was trained and evaluated using the DialogSum dataset from Hugging Face, containing dialogues and corresponding summaries. Despite efforts to fine-tune the model and train it for five epochs, the performance was unsatisfactory. Evaluation using Rouge metrics revealed poor summarization quality and low performance. 

#### Experimentation with Samsum Dataset  
Subsequently, the model was trained and evaluated using the Samsum dataset, which consists of dialogues and summaries. The dataset comprised 14,732 samples for training and 819 samples for testing. Utilizing the PEFT technique with this dataset resulted in remarkable improvements in summarization quality and performance. 


### 2- Next Word Prediction Model (Microsoft/DialoGPT-medium)

The initial attempt to gather data from the internet for the Next Word Prediction Model encountered limitations due to the scarcity and lack of specificity of available medical text. In response, a curated collection comprising 75 medical books and papers was assembled to serve as a richer and more domain-specific dataset.
To optimize this dataset for model training, conventional preprocessing methods proved insufficient. Consequently, a sophisticated approach known as Knowledge Distillation was employed. 

#### Knowledge Distillation Explanation : 
Knowledge Distillation (KD) is a promising technique for reducing the high computational demand of large language models (LLMs). However, previous KD methods are primarily applied to white-box classification models or training small models to imitate black-box model APIs like ChatGPT. How to effectively distill the knowledge of white-box LLMs into small models  
This involved utilizing the pretrained "teacher" model, specifically, the Zephyr-7b-alpha model. The teacher model was tasked with cleaning and extracting sentences suitable for fine-tuning a medical model. This process was guided by a prompt instructing the model to organize the text into suitable sentences, ready for fine-tuning.

Each book was processed by splitting it into paragraphs of length 512 tokens to facilitate efficient processing. On average, this processing task required 6 to 12 hours per book. The output from each book was consolidated into a unified dataframe, preparing it for fine-tuning with the student model, Microsoft/DialoGPT-medium.

The collective dataset, comprising 75 medical books and papers, yielded an average of 226,512.43 words and 23,882.26 lines 

### 3- Medical Chatbot Model (Microsoft/DialoGPT-medium)

The dataset was obtained from Health360 and consists of medical questions and answers extracted from medical books, reports, and other authoritative sources. This comprehensive dataset serves as the foundation for training and fine-tuning the language model to perform specific medical tasks effectively.
