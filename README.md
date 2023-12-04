# Summary
This repository contains solution to the task of identifying the names of mountains in the text. For training I use a Named Entity Recognition (NER) model, namely BERT with SpaCy, which automatically identifies 
and recognizes predefined entities (mountain's names in a given text and others). I use notebook **run.ipynb** as main file in EDA below, with comments and plots.

# Repository content
```
 ├── run.ipynb 
 ├── train.py         
 ├── inference.py
 ├── requirements.txt
 ├── outputs
      ├── eval_results.txt
```     

Firstly, download the dataset, using **load_dataset("DFKI-SLT/few-nerd", "supervised")** from **datasets**.
The dataset contains 3 sets of data: train, validation and test.

![11](https://github.com/yuliadziuba/Mountain_detection/assets/151251662/7afb40a9-8957-4586-831d-48f126ed7fd3)
```
1.run.ipynb notebook with descriptions, comments and plots
2.train.py consists of data balancing and data pre-processing before training, and also the training 
3.inference.py presentation of the result
4.requirements.txt contains necessary libraries/packages with corresponding versions
5.outputs/eval_results.txt contains metrics to evaluate the model
```
## Installation
Install dependencies

**pip3 install -r requirements.txt**

Run training part and visualization of results

**python train.py & python inference.py**

# EDA
Train, test and validation sets consist of **id, tokens, ner_tags, fine_ner_tags**. We are interested in the number that corresponds to **location-mountain**, only **fine_ner_tags** contains it and it's number **24**.
![22](https://github.com/yuliadziuba/Mountain_detection/assets/151251662/13b0affd-7b07-495f-8733-8f5ccfd094a9)

First of all, we need to balance the data, since the ratio of sentences that contain mountain names to those that don't is almost 1:100.

![77](https://github.com/yuliadziuba/Mountain_detection/assets/151251662/1dd54c55-17c9-4b02-a581-60465c875771)

Let's make a 1:1 ratio for each dataset.

Secondly, let's use the BIO (Beginning, Inside, Outside) format for tagging tokens. 

![33](https://github.com/yuliadziuba/Mountain_detection/assets/151251662/e863f12d-67a9-4075-a427-dc8e9648d5ab)

For example, the sentance  *"I visited the Everest Mountains when I was a child."* after the labeling will look like

![image](https://github.com/yuliadziuba/Mountain_detection/assets/151251662/256bc4aa-9f6d-49e4-afe8-c1d22d95dd0b)

After some pre-processing the data, we will start training the model.

# Architecture
I use Bert Model for NER which is able to convert unstructured data into structured data, using the above tags. I used the following parameters for model

![33333](https://github.com/yuliadziuba/Mountain_detection/assets/151251662/f34147ea-c24c-4b6f-a765-133d073a1b19)

Below we can see which metrics for model estimate I use. Of course, an important part of model building is specifying the loss function. The loss function is used to quantify the error between predicted and actual outputs at each step. The loss function plays a large role in how the model behaves and converges. Also precision and recall as a measure of quality and quantity. And F1 score as a harmonic mean of precision and recall. Also F1 useful for unbalanced data, which is our case.

![948](https://github.com/yuliadziuba/Mountain_detection/assets/151251662/fabd8b8a-fc2b-4a17-8e0d-5c4990719c35)

I think it's worth a try improving the accuracy by training the BERT model for more number of epochs or tuning other parameters such as learning rate, batch size, etc. However, they require high computational power and it takes a huge time to train a model, thus fine-tuning is the best approach to overcome the challenges.
