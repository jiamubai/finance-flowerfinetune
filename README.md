# FlowerTune LLM on Medical Dataset

This directory conducts federated instruction tuning with a pretrained Qwen-2.5-7B (https://huggingface.co/Qwen/Qwen2.5-7B) model on a Finance dataset.
We use [Flower Datasets](https://flower.dev/docs/datasets/) to download, partition and preprocess the dataset.
Flower's Simulation Engine is used to simulate the LLM fine-tuning process in federated way,
which allows users to perform the training on a single GPU.


## Methodology

This baseline performs federated LLM fine-tuning with [LoRA](https://arxiv.org/pdf/2106.09685) using the [🤗PEFT](https://huggingface.co/docs/peft/en/index) library.
The clients' models are aggregated with either FedAvg or FlexLoRA strategy. 

## Environments setup

Project dependencies are defined in `pyproject.toml`. Install them in an activated Python environment with:

```shell
pip install -e .
```

## Experimental setup

The dataset is divided into 20 partitions in an IID fashion, a partition is assigned to each ClientApp.
We randomly sample a fraction (0.1) of the total nodes to participate in each round, for a total of `10` rounds.
All settings are defined in `pyproject.toml`. To run experiments with flexlora, set `use_flexlora` to `1`.

## Evaluation Result


|          | fiqa  |  fpb  | tfns  | Average |
|:--------:|:-----:|:-----:|:-----:|:-------:|
|  FedAvg  | 74.34 | 76.98 | 83.29 |  78.20  |
| FlexLoRA | 75.00 | 83.16 | 80.02 |  79.39  |


## Model saving

The PEFT checkpoint can be found in: https://drive.google.com/file/d/1XuUdI36Ue3nwG1qVLlEQL1-m2fbewf0N/view?usp=sharing


