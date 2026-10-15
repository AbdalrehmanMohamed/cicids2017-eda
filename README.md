# Network Traffic EDA and Preprocessing for Intrusion Detection (CICIDS2017)

**Label: Academic** (team capstone project)

## Context
Capstone project on network intrusion (anomaly) detection using the public CICIDS2017 dataset. My part: Data & EDA Lead.

## Problem
Understand the traffic, find patterns that separate normal from malicious flows, and turn raw flows into clean, time-ordered windows that a sequence model can learn from.

## What I did
- Loaded 8 capture files (3.1M flows, 85 columns) and cleaned them: removed NaN/infinite values, exact duplicates (9.3%) and constant columns, leaving 2.83M flows
- Fixed timestamps (day-first dates, mixed formats, 12-hour clock without AM/PM) so flows sort in true time order
- Explored class imbalance (73% benign / 27% attack, 14 attack types), skewed features, attack timing and source-IP patterns
- Dropped highly correlated features and built sliding windows of 10 consecutive flows, split by day to avoid temporal leakage

## Key findings
- Features are extremely right-skewed, so a signed log transform is needed
- Attacks come in bursts, which justifies windows of consecutive flows instead of single rows
- One IP (172.16.0.1) sends over 554K attack flows, so identifiers like IPs and Flow ID would leak the label and were excluded
- No single feature separates attacks well (max correlation with the label about 0.5), so a multi-feature model is needed

## Files
- `01_eda_preprocessing.ipynb`: EDA and preprocessing
- `src/`: helper modules used by the notebook
