# LayoutLMv2
**Multimodal (text + layout/format + image) pre-training for document AI**

## Introduction
LayoutLMv2 is an improved version of LayoutLM with new pre-training tasks to model the interaction among text, layout, and image in a single multi-modal framework. It outperforms strong baselines and achieves new state-of-the-art results on a wide variety of downstream visually-rich document understanding tasks, including , including FUNSD (0.7895 → 0.8420), CORD (0.9493 → 0.9601), SROIE (0.9524 → 0.9781), Kleister-NDA (0.834 → 0.852), RVL-CDIP (0.9443 → 0.9564), and DocVQA (0.7295 → 0.8672).

[LayoutLMv2: Multi-modal Pre-training for Visually-Rich Document Understanding](https://arxiv.org/abs/2012.14740)
Yang Xu, Yiheng Xu, Tengchao Lv, Lei Cui, Furu Wei, Guoxin Wang, Yijuan Lu, Dinei Florencio, Cha Zhang, Wanxiang Che, Min Zhang, Lidong Zhou, [ACL 2021](#)

## Models
layoutlmv2-base-uncased | [huggingface](https://huggingface.co/microsoft/layoutlmv2-base-uncased)

## Installation

~~~bash
conda create -n layoutlmv2 python=3.7
conda activate layoutlmv2
git clone https://github.com/microsoft/unilm.git
cd layoutlmv2
pip install -r requirements.txt
pip install -e .
~~~

## Fine-tuning Example

### Sequence Labeling Task
We give a fine-tuning example for sequence labeling tasks. You can run this example on [FUNSD](https://guillaumejaume.github.io/FUNSD/), a dataset for document understanding tasks.
~~~bash
# Suppose you have 4 GPUs. 
python -m torch.distributed.launch --nproc_per_node=4 experiments/run_funsd.py \
        --model_name_or_path microsoft/layoutlmv2-base-uncased \
        --output_dir /tmp/test-ner \
        --do_train \
        --do_predict \
        --max_steps 1000 \
        --warmup_ratio 0.1 \
        --fp16
~~~

### Results

#### FUNSD (entity-level)

| Model                         | Precision  | Recall     | F1         |
| ----------------------------- | ---------- | ---------- | ---------- |
| `bert-base-uncased`           | 0.5469     | 0.6710     | 0.6026     |
| `unilmv2-base-uncased`        | 0.6349     | 0.6975     | 0.6648     |
| `layoutlm-base-uncased`       | 0.7597     | 0.8155     | 0.7866     |
| **`layoutlmv2-base-uncased`** | **0.8029** | **0.8539** | **0.8276** |

## Citation

If you find LayoutLMv2 useful in your research, please cite the following paper:

``` latex
@inproceedings{Xu2020LayoutLMv2MP,
  title     = {LayoutLMv2: Multi-modal Pre-training for Visually-Rich Document Understanding},
  author    = {Yang Xu and Yiheng Xu and Tengchao Lv and Lei Cui and Furu Wei and Guoxin Wang and Yijuan Lu and Dinei Florencio and Cha Zhang and Wanxiang Che and Min Zhang and Lidong Zhou},
  booktitle = {Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics (ACL) 2021},
  year      = {2021},
  month     = {August},
}
```

## License

The content of this project itself is licensed under the [Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
Portions of the source code are based on the [transformers](https://github.com/huggingface/transformers) project.
[Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct)

### Contact Information

For help or issues using LayoutLMv2, please submit a GitHub issue.

For other communications related to LayoutLMv2, please contact Lei Cui (`lecu@microsoft.com`), Furu Wei (`fuwei@microsoft.com`).

