# Working with ReCoRD Data

Note, 10/04/2019: In order to work with the Record dataset, it's best viewed as a multi-label problem. You need to account for multiple possible entities as answers to any one question (fill in the blank, really). This is a tricky model to implement for a variety of reasons. Here are a few approaches which could be taken and their negative effects:

- If you create multiple copies of a question and answer combinations ([CLS] + question + [SEP] + passage + [SEP] + entity) and turn it into a binary classification problem, you end up with a enormous dataset. (This is the approach implemented in this repository/notebook)

- If you can take a model such as ```model = BertForMultipleChoice.from_pretrained("bert-base-uncased")```, you end up with sequences which are too large for our model to accept. [See example here with Swag dataset](https://github.com/huggingface/transformers/blob/f2a3eb987e1fc2c85320fc3849c67811f5736b50/examples/single_model_scripts/run_swag.py)

- If you take a Question Answering model, you have to account for multiple combinations of starting and ending indices. [See my example with Squad here](https://github.com/devkosal/fastai_roberta/blob/other_tasks/fastai_roberta_squad/BERT%20with%20Fastai%20-%20SQuAD.ipynb) This may be the most promising approach. 