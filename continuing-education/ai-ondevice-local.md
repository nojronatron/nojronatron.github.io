# Spotlight On Device and Local AI Reactor Presentation

Notes taken from a Microsoft Reactor "Model Mondays" presentation about local AI features and usage.

## Hosts

Maanav Dalal, Product Manager, Core AI, Microsoft

Sharmila Chockalingam, Senior PMM, Azure AI

## Azure AI Foundry Highlights

RFT: Adjusts model weights using a grader (rewards) to score outputs against reference data.

- Steers model reasoning direction
- Penalizes incorrect or undesireable outcomes
- SFT: Supervised Fine Tuning

Github Spark:

- Now in public preview
- Less auto-complete, more mind-reading pair programmer

DAViD:

- Data efficient and Accurate Vision Models from Synthetic Data
- Lower cost on training compared to foundational models

Agent Experience Optimization:

- Simplify content discovery
- Related to NLWeb

## Main Topic Notes

Demo: Foundry

- Manages AI Models
- Can list available models
- Run model for interactive mode

Demo: RAG

- Upload documents to process them as part of the RAG "knowledge base"
- Query RAG to extract data from the uploaded documents

## Customer Stories

Xander:

- Working to solve acacessibility issues
- Capturing Classes/AR Glasses
- Real-time captions
- Run on the Edge
- Computing power on the glasses themselves
- Embedded Speech SDK
- MSFT Embedded SDK
- Veterans support (VA) scenrio is focus: Lack of internet, brain injuries (effasia), tinnitus
- Diarization: Identifying speakers among multiple simultaneous speakers
- Glasses ship with models pre-loaded so customers do not need to do model setup tasks

Demo:

- Running 5 SLMs
- Using Azure AI Edge
- Information fed to Azure Edge AI for processing
- Processed data returned to glasses for display (captioning)
- Challenges occur with rapid caption display: Hard to keep up with, and those with cognitive issues
- Captions words even in noisy environments
- Partial Fragment processing vs Completed Fragment processing
