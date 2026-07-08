# Beyond Self‑Knowledge: Propagating Uncertainty Across Reasoning and Retrieval in LLMs (BeyondUncertainty)

<p align="center">
   <img alt="GitHub License" src="https://img.shields.io/github/license/Rocky5502/BeyondUncertainty">
   <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/Rocky5502/BeyondUncertainty">
   <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/Rocky5502/BeyondUncertainty">
</p>

<p align="center">
   📃 <a href="https://arxiv.org/abs/????">Paper</a> • 🤗 <a href="#datasets">Datasets</a>
</p>

This repository extends and generalizes the codebase of the ACL 2025 paper **Adaptive Retrieval Without Self‑Knowledge? Bringing Uncertainty Back Home** to support our AAAI 2027 submission **Beyond Self‑Knowledge: Propagating Uncertainty Across Reasoning and Retrieval in LLMs**.  While **AdaRAGUE** focused on adaptive retrieval triggered by a single uncertainty estimate at the final answer, our work investigates how uncertainty evolves across intermediate reasoning steps and shows how step‑level uncertainty can drive retrieval, early stopping, or answer abstention.  

The code here is based on the original `AdaRAGUE` repository but has been renamed and lightly refactored to reflect our new research focus.  We retain the same datasets, methods, and evaluation scripts so that researchers can reproduce our results and compare them with prior adaptive retrieval approaches.  We also provide a new framework implementation that propagates uncertainty through reasoning and retrieval, along with instructions for integrating alternative language models such as ChatGPT, Gemini or Claude.

## BeyondUncertainty framework

![BeyondUncertainty Framework](figures/framework.pdf)

The figure above summarizes our proposed **BeyondUncertainty** framework.  Given a question and an initial context, an LLM performs multi‑step reasoning and produces a step‑level uncertainty estimate after each step.  An uncertainty‑aware controller aggregates these step uncertainties and decides whether to:

- **Continue reasoning** when uncertainty decreases and the answer appears reliable;
- **Trigger external retrieval** when uncertainty increases, fetching additional evidence that is injected back into the reasoning process;
- **Stop early** if the answer is confidently known without further reasoning or retrieval; or
- **Abstain** from answering if uncertainty remains high after several steps.

By propagating uncertainty across the reasoning trajectory, the model can adaptively use retrieval only when it is needed, reducing cost and improving answer reliability.  For more details please see the paper and the `beyond_uncertainty_framework.py` implementation included in this repository.

## Repository structure

The project preserves the structure of the original `AdaRAGUE` codebase.  Below is a high‑level overview:

```
data/                 # train and test splits for each dataset (HotpotQA, 2wikimultihopQA, SQuAD, TriviaQA, MuSiQue, Natural Questions)
standard_retriever/   # unified retriever for all methods, based on ElasticSearch and Wikipedia
Adaptive_Rag/         # code for baseline Adaptive RAG and IRCoT methods
SeaKR/                # SeaKR method with uncertainty estimation tweaks
dragin/               # FLARE/DRAGIN implementations
rowen/                # Rowen method
UC/                   # uncertainty estimation methods used in evaluation
figures/              # figures used in the paper (framework and motivational examples)
scripts/              # helper scripts to run experiments (see method README files)
```

We renamed the repository from **AdaRAGUE** to **BeyondUncertainty**.  All existing method implementations are kept intact to allow fair comparisons.  You can still run each method following the instructions in the corresponding subfolder (`Adaptive_Rag/README.md`, `SeaKR/README.md`, `dragin/README.md`, etc.).  The only differences are the new framework implementation and updated documentation reflecting our research questions.

## Installation

We recommend using Python 3.10+ and creating a separate virtual environment.  The repository contains `requirements.txt` or `pyproject.toml` files in each method subfolder specifying the dependencies.  You should first install the retriever and build the Wikipedia index:

```bash
cd standard_retriever
pip install -r requirements.txt  # install ElasticSearch and other dependencies
python build_wiki_index.py --dump_path /path/to/wikipedia/dump --index_dir /path/to/index
```

Next, choose a method to evaluate.  For example, to run our proposed framework you can install the uncertainty estimation code and run the controller:

```bash
cd UC
pip install -r requirements.txt

# run uncertainty estimation on a dataset
bash bin/run_uncertainty.sh --dataset hotpotqa --model gpt-4 --framework beyond_uncertainty
```

Each method folder contains its own `README.md` with detailed instructions and hyperparameters.  For evaluating alternative LLMs (e.g., ChatGPT, Gemini or Claude) you can modify the `--model` flag accordingly.  Our framework is model‑agnostic: as long as your LLM exposes a function to produce intermediate reasoning steps and uncertainty estimates, you can plug it into the controller.

## Datasets

We use standard open‑domain QA datasets: Natural Questions, HotpotQA, 2wikimultihopQA, SQuAD, TriviaQA and MuSiQue.  For our experiments we sample 500 questions from each dataset (see `data/` for the splits).  You can substitute other datasets by creating similar CSV files with columns `id,question,context,answer`.

## Contributing

If you adapt our framework, add a new uncertainty estimator, or evaluate additional language models, feel free to open an issue or a pull request.  We welcome contributions that improve the usability and reproducibility of the codebase.

## Citation
Coming soon 
If you use this code or refer to ideas from our paper, please cite:

```bibtex
@inproceedings{beyondUncertainty2026,
  title={Beyond Self-Knowledge: Propagating Uncertainty Across Reasoning and Retrieval in Large Language Models},
  author={Sah, Chandan Kumar and Lian, Xiaoli and Zhang, Li },
  year={2026},
  journal={arXiv preprint coming soon,
}
```
