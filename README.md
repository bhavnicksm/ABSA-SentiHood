# ABSA-SentiHood

This repository was made as a submission for IIIT Delhi MIDAS lab task. 

## About the Dataset

The dataset is found under the data section of the repository and contains the following files:

```file
|
+-- data
    +-- sentihood-train.json
    +-- sentihood-dev.json
    +-- sentihood-test.json
```


## Approach
The approach taken here was completely based on [1]; the approach essentially frames the aspect-based sentiment analysis (ABSA) question as either a QA task or a NLI task. Given the constraints of time and efficiency, NLI task was chosen as the main focus of this approach, specifically NLI-M task (which stands for NLI multi-label classification)

## Experiments

The models were trained with the following HF Trainer Arguments on a Google Colab Notebook (present in the notebooks folder):

```python
TrainingArguments(output_dir = f"/content/drive/MyDrive/SentiHood/models/{model_name}",
                  overwrite_output_dir = True,
                  num_train_epochs = 5,
                  evaluation_strategy="steps",
                  eval_steps=500,
                  logging_steps=500, 
                  per_device_train_batch_size = 8,
                  per_device_eval_batch_size = 8,
                  learning_rate = 5e-6,
                  warmup_ratio = 0.1,
                  weight_decay = 0.01,
                  save_strategy = 'epoch',
                  seed = 42,
                  )

```

| Model Name | Test-Accuracy | Test-Recall | Test-Precision | Test-F1 |
| --- | --- | --- | --- | --- |
| bert-base-uncased | 0.9822546389447798 | 0.8411322714846929 | 0.8733654497362174 | 0.8567007821344529 |
| roberta-base | 0.9830371115582384 | 0.8531581122933095 | 0.8630080220007996 | 0.8578191613396783 |


## Code


## References

[1] [Utilizing BERT for Aspect-Based Sentiment Analysis
via Constructing Auxiliary Sentence](https://aclanthology.org/N19-1035.pdf)


## License
[MIT](https://choosealicense.com/licenses/mit/)