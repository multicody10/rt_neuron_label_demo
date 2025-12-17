## What this is
* A minimal end to end loop you can run locally
* A template you can adapt to real model activations or real neural pipelines later
# Real time neuron labeling demo

A small runnable demo that treats labeling as an online inference loop:

* stable identity tracking under drift
* streaming feature extraction
* streaming functional labeling into NeuronCards with confidence
* active probing that selects the next stimulus and state to reduce uncertainty

This repo has two demos:

* **Bio style analog** (`src/`): synthetic spike counts with hidden tuning plus identity drift
* **AI unit labeling** (`src_ai/`): streaming concept conditioned labeling for hidden units in a toy model
## Repo layout

```text
requirements.txt
LICENSE.txt

src/
  simulator.py           Synthetic population and hidden tuning generator
  identity_tracker.py    Stable ID matching under drift
  online_labeler.py      Streaming label vectors + confidence
  active_prober.py       Chooses next probes to reduce label uncertainty
  run_console.py         Console runner
  run_dashboard.py       Streamlit dashboard

src_ai/
  dataset.py             Streaming concept labeled inputs
  toy_model.py           Small feedforward toy model
  online_labeler_ai.py   Streaming unit labeling against concepts
  run_ai_demo.py         AI demo runner

paper_assets/
  fig1_pipeline.png
  fig2_snapshot.png
```

## How this addresses the NeuronAI issue

The NeuronAI problem is: you do not want vague interpretability stories, you want a system that can keep a stable handle on each unit and attach a functional label that updates in real time.

This repo solves that by turning neuron labeling into an online loop with four concrete pieces:

1. Stable identity
   * `src/identity_tracker.py` keeps a persistent id for each unit even when features drift, so labels stick to the same neuron over time instead of renumbering.

2. Streaming labeling, not one shot labeling
   * `src/online_labeler.py` and `src_ai/online_labeler_ai.py` maintain running statistics per unit, so every new observation updates the NeuronCard immediately.

3. Label vectors with confidence
   * Each unit gets a NeuronCard that stores a label profile and confidence, not a single brittle tag. This is the practical version of “label every neuron”.

4. Active probing to reduce uncertainty
   * `src/active_prober.py` chooses the next stimulus or state to test based on which probes will disambiguate competing labels fastest. This is how you scale labeling without brute force.

In short: every unit has (a) a stable id, (b) a live profile of what it responds to, (c) confidence scores, and (d) an experiment loop that improves the labels online.


## What this is not
* Not a medical device
* Not a brain interface
* Not a spike sorter for electrode data

## Requirements
* Python 3.10 or newer

## Quick start on Windows
PowerShell in the repo root:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```
### from repo root
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```
### AI unit labeling demo
```powershell
python src_ai\run_ai_demo.py
```
### bio style console demo
```powershell
python src\run_console.py
```
### bio style dashboard
```powershell
streamlit run src\run_dashboard.py
```
