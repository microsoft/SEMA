Official Repository of

**SEMA**: **S**imple yet **E**ffective Learning for **M**ulti-Turn Jailbreak **A**ttacks
[![Paper](https://img.shields.io/badge/arXiv-2602.06854-b31b1b.svg)](https://arxiv.org/abs/2602.06854)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Venue](https://img.shields.io/badge/ICLR-2026-green.svg)](https://arxiv.org/abs/2602.06854)

and

**SEMA-Auto**: **S**ighted and **E**fficient **M**ulti-Turn **A**ttack with **Auto**nomy
[![Paper](https://img.shields.io/badge/arXiv-2602.06854-b31b1b.svg)](https://arxiv.org/abs/2610.35743)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)


# SEMA-Auto
The code is currently undergoing review for release and is coming soon.


# SEMA

SEMA is a framework for training open-loop, response-agnostic multi-turn jailbreak attackers via **Prefilling Self-Tuning** and **Reinforcement Learning with Intent-drift-aware Reward**. Unlike closed-loop methods, SEMA eliminates the need for real-time victim-model feedback during attack generation.

## Installation

### Docker (recommended)

```bash
docker pull allenlao/sema:v0.1
docker run --gpus all --name sema -it \
  --ipc=host \
  --ulimit memlock=-1 \
  --ulimit stack=67108864 \
  allenlao/sema:v0.1
```

### From source

```bash
conda create -n sema python=3.12.3 -y
conda activate sema
pip install -r requirements.txt
# Please make sure the CUDA 12.6 toolkit is available
```
Note that we developed against CUDA 12.6; higher versions of CUDA may not be compatible.

## Set Up API Keys
Create a `.env` file in the root directory of this repository and store your API keys there, along with any other environment variables you need. Our training uses GPT to provide part of the reward signal, so `OPENAI_API_KEY` is required. For example:
```
OPENAI_API_KEY=your-openai-key-here
```

Please also make sure you are logged in to Hugging Face and Weights & Biases:
```
huggingface-cli login
wandb login
```

## Quick Start

**Stage I** — Prefilling Self-Tuning (generates rollouts, then fine-tunes the attacker):

```bash
bash scripts/prefill_selftuning_llama8b_4x80gb-gpu.sh
```

**Stage II** — RL with Intent-drift-aware Reward (trains against a victim model):

```bash
bash scripts/rl_ida_llama8b@llama8b_8x80gb-gpu.sh
```

The AdvBench dataset is downloaded automatically on first run. Outputs are saved to `files/`.

See [examples/](examples/) for all available training configurations and [docs/](docs/) for detailed documentation.

## Documentation

| Document | Description |
|----------|-------------|
| [Architecture](docs/architecture.md) | Project structure, modules, and data flow |
| [Training Pipeline](docs/training.md) | Detailed Stage I & II training guide |
| [Reward System](docs/rewards.md) | Intent-drift-aware reward and ablations |
| [Configuration](docs/configuration.md) | Hyperparameters and hardware requirements |

## Citation

If you use SEMA in your research, please cite:


```bibtex
@inproceedings{sema2026,
      title={SEMA: Simple yet Effective Learning for Multi-Turn Jailbreak Attacks}, 
      author={Mingqian Feng and Xiaodong Liu and Weiwei Yang and Jialin Song and Xuekai Zhu and Chenliang Xu and Jianfeng Gao},
      year={2026},
      booktitle={International Conference on Learning Representations (ICLR)},
      eprint={2602.06854},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2602.06854}
}
```

## Contact

For any questions regarding the package or paper, feel free to reach out to:

- **Mingqian Feng** - mingqian.feng@rochester.edu
- **Weiwei Yang** - weiweiy@microsoft.com
- **Carolyn Buractaon** - caburact@microsoft.com
- **Xiaodong Liu** - xiaodl@microsoft.com

## License

MIT License — see [LICENSE](LICENSE) for details.

