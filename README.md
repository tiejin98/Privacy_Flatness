# Privacy_Flatness

## Acknowledgement
Our code is based on [link](https://github.com/lxuechen/Differentially-Private-Fine-tuning-of-Language-Models). Thanks for their excellent work.

## Requirement
please install all requirement by using ```pip install -r requirements.txt```. We also update peft package with our code. So please replace the original **mapping.py** and **peft_model.py** with the code in this repo.

## Datasets
For the classification task, cd *LLM_dp/private-transformers/examples/classification/data* and using ```bash download_dataset.sh``` to download the dataset. 

## Privacy-Flat
To run the code, first cd *private-transformers/examples* 

```python3 -u -m classification.run_wrapper_pretuning_sparse_real --output_dir /home/tchen169/private-transformers/examples/classification/sst2-eps3 --task_name sst-2 --num_train_epochs 10 --target_epsilon 3 --model_name_or_path roberta-base --few_shot_type prompt --batch_size 1024 --learning_rate 5e-5 --non_private yes```

It will generate one **.pt** file end with **_sparse** to guide training. After that, use the following command to get results for our method.

```python3 -u -m classification.run_wrapper_pretuning_final --output_dir /home/tchen169/private-transformers/examples/classification/reg --seed 1 --target_epsilon 3 --task_name sst-2 --num_train_epochs 30  --model_name_or_path roberta-base --few_shot_type prompt --batch_size 1024 --learning_rate 5e-5```

Currently, the sparse layers are selected based on roberta-base. It is possible to change the remove layer list in **run_classification_pretuning_final.py** and **run_classification_pretuning_sparse.py** and you may use **classification.run_wrapper_pretuning_flat** to get more the information about which layer to remove.












