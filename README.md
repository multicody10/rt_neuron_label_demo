# Real time neuron labeling demo

A small runnable demo that treats labeling as an online inference loop:

* stable identity tracking under drift
* streaming feature extraction
* streaming functional labeling into NeuronCards with confidence
* active probing that selects the next stimulus and state to reduce uncertainty

This repo has two demos:

* **Bio style analog** (`src/`): synthetic spike counts with hidden tuning plus identity drift
* **AI unit labeling** (`src_ai/`): streaming concept conditioned labeling for hidden units in a toy model

## What this is
* A minimal end to end loop you can run locally
* A template you can adapt to real model activations or real neural pipelines later

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
