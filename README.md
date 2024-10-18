# OpenLTSM (Open-Source Large Time Series Models)

Implementations of large time series models, as well as pre-training datasets, adaptation techniques, and new benchmarks.

> [!NOTE]
> OpenLTSM is currently under a rapid development intending to explore the design philosophy of large foundation models in the time series field. It is not intended to be completely compatiable with official codebases and existing checkpoints. (It is also welcome for any interested one to provide interesting works and PR :)

We aim to provide a neat codebase to **develop and evaluate** large time series models, which typically covers three milestone of tasks: **supervised training**, **large-scale pre-training**, and **large model adaptation**.

> For deep time series models and supervised benchmark, we strongly recommend [Time-Series-Library](https://github.com/thuml/Time-Series-Library) and this comprehensive [Suvery](https://arxiv.org/abs/2407.13278).

:triangular_flag_on_post: **News** (2024.10) We include four large time series models, release the pre-training datasets/dataloaders, and provide evaluation scripts.

## Model Checklist

- [x] **Moirai** - Unified Training of Universal Time Series Forecasting Transformers. [[ICML 2024]](https://arxiv.org/abs/2402.02592), [[Code]](https://github.com/SalesforceAIResearch/uni2ts)
- [x] **Moment** - MOMENT: A Family of Open Time-series Foundation Model. [[ICML 2024]](https://arxiv.org/abs/2402.03885), [[Code]](https://github.com/moment-timeseries-foundation-model/moment)
- [x] **Timer** - Timer: Generative Pre-trained Transformers Are Large Time Series Models. [[ICML 2024]](https://arxiv.org/abs/2402.02368), [[Code]](https://github.com/thuml/Large-Time-Series-Model)
- [x] **Timer-XL** - Timer-XL: Long-Context Transformer for Unified Time Series Forecasting. [[arxiv 2024]](https://arxiv.org/abs/2410.04803), [[Code]](https://github.com/thuml/Timer-XL)

> We will update the followin models to the checklist after a comprehensive evaluation. Welcome to give your suggestion about interesting works 🤗

- [ ] **AutoTimes** - AutoTimes: Autoregressive Time Series Forecasters via Large Language Models. [[NeurIPS 2024]](https://arxiv.org/abs/2402.02370), [[Code]](https://github.com/thuml/AutoTimes)
- [ ] **Chronos** - Chronos: Learning the Language of Time Series. [[arxiv 2024]](https://arxiv.org/abs/2403.07815), [[Code]](https://github.com/amazon-science/chronos-forecasting)
- [ ] **Time-MoE** - Time-MoE: Billion-Scale Time Series Foundation Models With Mixture Of Experts. [[arxiv 2024]](https://arxiv.org/abs/2409.16040), [[Code]](https://github.com/Time-MoE/Time-MoE)
- [ ] **TimesFM** - A Decoder-Only Foundation Model for Time-Series Forecasting. [[arxiv]](https://arxiv.org/abs/2310.10688), [[Code]](https://github.com/google-research/timesfm)


## Usage


1. Install Python 3.10. For convenience, execute the following command.

```
pip install -r requirements.txt
```

1. Place the downloaded data in the folder ```./dataset```. Here is a [dataset summary](./figures/datasets.png).

* **For pre-training**:
  * [UTSD](https://huggingface.co/datasets/thuml/UTSD) for domain-universal pre-training. A large version is on the way!
  * [ERA5-Familiy](https://www.ecmwf.int/en/forecasts/dataset/ecmwf-reanalysis-v5) for domain-specific pre-training (will soon be released).
* **For supervised training / generalization**: We use datasets from [TSLib](https://github.com/thuml/Time-Series-Library), which are accessible in [[Google Drive]](https://drive.google.com/drive/folders/13Cg1KYOlzM5C7K8gK8NfC-F3EYxkM3D2?usp=sharing) or [[Baidu Drive]](https://pan.baidu.com/s/1r3KhGd0Q9PJIUZdfEYoymg?pwd=i9iy)

2. Pre-train and evaluate large model. We provide the experiment scripts for all benchmarks under the folder `./scripts/`. You can reproduce the experiment results as the following examples:

```
# Supervised training
# (1) one-for-one forecast
bash ./scripts/supervised/forecast/moirai_ecl.sh
# (2) one-for-all forecast
bash ./scripts/supervised/rolling_forecast/timer_xl_ecl.sh

# Large-scale pre-training
# (1) pre-training on UTSD
bash ./scripts/pretrain/ETT_script/timer_xl_utsd.sh
# (2) pre-training on ERA5
bash ./scripts/pretrain/ETT_script/timer_xl_era5.sh

# Large model adaptation (will released soon)
# (1) full-shot fine-tune
# (2) few-shot fine-tune
# (3) zero-shot generalization
```

3. Develop your own large model.

- Add the model file to the folder `./models`. You can follow the `./models/timer.py`.
- Include the newly added model in the `Exp_Basic.model_dict` of  `./exp/exp_basic.py`.
- Create the corresponding scripts under the folder `./scripts`.


## Leaderboard (In-Process)

## Efficiency (In-Process)
We present a [theoretical derivation](./figures/efficiency.png) of the computational complexity of Transformers on time series, including the parameter counts, memory footprint, and FLOPs.

## Citation

If you find this repo helpful, please cite our paper. 

```
@inproceedings{liutimer,
  title={Timer: Generative Pre-trained Transformers Are Large Time Series Models},
  author={Liu, Yong and Zhang, Haoran and Li, Chenyu and Huang, Xiangdong and Wang, Jianmin and Long, Mingsheng},
  booktitle={Forty-first International Conference on Machine Learning}
}

@article{liu2024timer,
  title={Timer-XL: Long-Context Transformers for Unified Time Series Forecasting},
  author={Liu, Yong and Qin, Guo and Huang, Xiangdong and Wang, Jianmin and Long, Mingsheng},
  journal={arXiv preprint arXiv:2410.04803},
  year={2024}
}
```

## Acknowledgement

We appreciate the following GitHub repos a lot for their valuable code and efforts:
- Time-Series-Library (https://github.com/thuml/Time-Series-Library)
- Large-Time-Series-Model (https://github.com/thuml/Large-Time-Series-Model)
- AutoTimes (https://github.com/thuml/AutoTimes)

## Contributors

If you have any questions or want to use the code, feel free to contact:
* Yong Liu (liuyong21@mails.tsinghua.edu.cn)
* Guo Qin (qinguo24@mails.tsinghua.edu.cn)