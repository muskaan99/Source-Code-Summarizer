# Code-Summarizer: 
The aim of the project is to create a deep learning model to generate a natural language summary of source code in python i.e. it will describe the functionality of a python program. The dataset consists of python docstrings and code. We compared the performance of three models: a pre-trained RoBERTa model, a pre-trained CodeT5 model and our custom model. The models will be compared based on two performance metrics: BLEU score and EM score. 

# Steps to follow to run Code Summarizer:

1. Clone the repo

2. Python Packages to be installed (recommend running pip3 install --upgrade pip before installing the below packages) : 
 - torch 
 - tensorboard
 - tree-sitter
 - transformers
 - gsutil 

3. Run the below command inside the working directory of code-summarizer repo to download the data

```
gsutil -m cp -r "gs://sfr-codet5-data-research/data" .
```

Optional: You can download the pre-trained and fine-tuned models using the below commands.

```
gsutil -m cp -r "gs://sfr-codet5-data-research/pretrained_models" .
```

```
gsutil -m cp -r "gs://sfr-codet5-data-research/finetuned_models" .
```

4. Change the working directory inside /sh/exp_with_args.sh (WORKDIR) to the path of your repository.
 
5. Batch sizes and number of epochs can be modified inside run_exp.py. The batch_size is set as 48 and can be changed inside run_exp.py. The training epochs can be set in the same file.


6. Set the python version according to the version on your machine.

7. To build on the Seq2Seq model, we use the model tag 'roberta' to get the exact errors printed on the terminal. 

8. Command to initiate training on the model : 

```
python3 run_exp.py --model_tag roberta --task summarize --sub_task python
```

```
python3 run_exp.py --model_tag roberta --task summarize --sub_task python
```

10. If you face an error similar to _AttributeError: module 'setuptools._distutils' has no attribute 'version'_ during training, it can be resolved by using the workaround 

```
pip3 install setuptools==59.5.0
```

# MLOps:

We have deployed one of our pre-trained models (CodeT5) on a web application which is running using Flask. A user can enter a code snippet in a text area on the web page and get a short description of the functionality of the code.

To run the web application:

```
cd mlops/flask
python3 web_app.py
```

# Model Files:
Custom Model: 

Model file: pytorch_model_custom_model.bin
Size: 529.518 MB


CodeT5 pretrained:

Model File: pytorch_model_codet5.bin
Size: 202.240 MB

Roberta Pretrained:

Model File: pytorch_model_roberta.bin
Size: 674 MB

## References
```
@inproceedings{
    wang2021codet5,
    title={CodeT5: Identifier-aware Unified Pre-trained Encoder-Decoder Models for Code Understanding and Generation}, 
    author={Yue Wang, Weishi Wang, Shafiq Joty, Steven C.H. Hoi},
    booktitle={Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing, EMNLP 2021},
    year={2021},
}
```
