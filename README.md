# ABSA-SentiHood

This repository was made as a submission for IIIT Delhi MIDAS lab task. 

ToDo List of Experiments:

- [x] bert-base NLI-M task  
- [x] roberta-base NLI-M task
- [ ] bert-large NLI-M task (currently running)
- [ ] roberta-large NLI-M task (currently running)
- [ ] electra-base NLI-M task
- [ ] bert-base NLI-B task  
- [ ] roberta-base NLI-B task
- [ ] bert-large NLI-B task 
- [ ] roberta-large NLI-B task 
- [ ] electra-base NLI-B task


## About the Dataset

The dataset is found under the data section of the repository and contains the following files:

```file
|
+-- data
    +-- sentihood-train.json
    +-- sentihood-dev.json
    +-- sentihood-test.json
```

The files contain the following number of examples: 


| file | Examples |
| --- | --- |
| Train | |
| Dev |  |
| Test | | 


## Approach
The approach taken here was completely based on [1](#references); the approach essentially frames the aspect-based sentiment analysis (ABSA) question as either a QA task or a NLI task. Given the constraints of time and efficiency, NLI task was chosen as the main focus of this approach, specifically NLI-M task (which stands for NLI multi-label classification)

## Experiments

The models were trained with the following HF Trainer Arguments on a Google Colab Notebook (present in the notebooks folder). Note that, by default HFTrainer uses the `AdamW` optimizer. 

```python
TrainingArguments(output_dir = f"/content/drive/MyDrive/SentiHood/models/{model_name}",
                  overwrite_output_dir = True,
                  num_train_epochs = 5,
                  evaluation_strategy="steps",
                  eval_steps=500,
                  logging_steps=500, 
                  per_device_train_batch_size = 8,
                  per_device_eval_batch_size = 8,
                  learning_rate = 5e-5,
                  warmup_ratio = 0.1,
                  weight_decay = 0.01,
                  save_strategy = 'epoch',
                  seed = 42,
                  )

```

| Model Name |Task Type| Test-Accuracy | Test-Recall | Test-Precision | Test-F1 |
| --- | --- | --- | --- | --- | --- |
| bert-base-uncased | NLI-M | 0.9822546389447798 | 0.8411322714846929 | 0.8733654497362174 | 0.8567007821344529 |
| roberta-base | NLI-M | 0.9830371115582384 | 0.8531581122933095 | 0.8630080220007996 | 0.8578191613396783 |


The final model chosen for submission is: **roberta-base**


## Submission

Since the use of proper GPUs for training of LLMs is necessary, the code was entirely written and executed in Google Colab Notebooks. Said notebooks can be found under the notebooks folder. 

The submissions for each model are contained in the submissions folder. Each submission is a `.jsonl` file having 1491 examples (in dictionaries) with the following structure.

```python
[
    {
        'id': 61,
        'opinions': [{'aspect': 'live',
               'sentiment': 'Positive',
               'target_entity': 'LOCATION1'}],
        'text': 'I really like LOCATION1  I lived there for 3 months and had a lot of fun',
        'model_pred': [{'aspect': 'live',
               'sentiment': 'Positive',
               'target_entity': 'LOCATION1'}]
    }
...
```


## References

[1] [Utilizing BERT for Aspect-Based Sentiment Analysis
via Constructing Auxiliary Sentence](https://aclanthology.org/N19-1035.pdf)

[2] [HuggingFace Trainer](https://huggingface.co/docs/transformers/main_classes/trainer#trainer)


## License
[MIT](https://choosealicense.com/licenses/mit/)