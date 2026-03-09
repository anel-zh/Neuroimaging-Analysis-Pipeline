# Modular Framework for fMRI-based Predictive Modeling

## Introduction

Functional MRI (fMRI) produces high-dimensional, 4D datasets in which neural signals evolve across both space and time. Transforming these thousands of spatial units and temporal acquisition points into structured inputs for predictive modeling presents significant computational challenges. This is further complicated by the need to precisely align continuous behavioral data with imaging acquisition sequences.

This repository provides a modular MATLAB pipeline designed for brain–behavior prediction using time-resolved neuroimaging data. The workflow standardizes the transition from raw data to predictive insights through reproducible stages: behavioral preprocessing, temporal alignment, denoising, neural feature extraction, dataset assembly, and cross-validated modeling.

## Project Motivation

A core objective of this pipeline is to bridge the gap between two traditionally separate analytical approaches: **activation-based** and **connectivity-based** modeling. While most neuroimaging workflows focus on one or the other, this framework integrates both within a unified predictive architecture.

The pipeline extracts and models two complementary feature families:

- **Activation features** derived via single-trial **Hemodynamic Response Function (HRF) regression** at the voxel or atlas-defined region level, capturing localized stimulus-evoked neural responses.
- **Connectivity features** computed using **Dynamic Conditional Correlation (DCC)**, a GARCH-based multivariate time-series method that estimates **time-varying functional interactions between brain regions**.

By combining these representations, the framework captures both **localized neural processing** and **large-scale network dynamics**. This dual-stream modeling approach enables direct comparison of each feature family’s predictive contribution while reducing multicollinearity and improving the interpretability of brain–behavior relationships.

## Methods

- Input Specifications: The pipeline expects preprocessed 4D fMRI data in BIDS format. It is optimized for data that has undergone ICA-AROMA or standard spatial smoothing.
- Data Preparation: Continuous behavioral ratings and fMRI time-series are temporally aligned and synchronized. Behavioral signals are interpolated and shifted to account for hemodynamic lag, ensuring precise correspondence with neural data.
- Flexible Feature Extraction: The workflow implements a modular denoising stage. It is designed to be flexible: regressing mean White Matter (WM) and CSF signals for ICA-cleaned data, or implementing an expanded 24-parameter motion model and Anatomical CompCor for standard smoothed data.
- Model Training: The framework evaluates 6 distinct models to compare predictive utility across feature families (Activation, Connectivity, and Combined) and run conditions (Task-only vs. Task + Rest). The training process is flexible, allowing for user-defined cross-validation schemes (e.g., Leave-One-Subject-Out) and dimensionality reduction parameters.

## Expected Results

The pipeline generates standardized outputs for each stage of the workflow:
- Extracted Features: Saved feature matrices containing binned HRF-based activation coefficients and time-resolved DCC connectivity estimates.
- Saved Model Architectures: Fully trained model structures for all 6 comparison variants, including optimized weights and intercept values.
- Performance Comparisons: Summary metrics (e.g., prediction-outcome correlation, MSE, and R2) comparing the predictive performance of different feature sets and run conditions.


## Repository Note

This public repository features a **demonstration version** of the pipeline using a sustained-pain fMRI case. While simplified to protect unpublished research findings, it preserves the core modular architecture and computational principles of the original pipeline. It serves as a scalable and reproducible template that can be adapted for diverse task-based or resting-state fMRI studies. Additional analytical outputs, including advanced results (e.g., bootstrap, variance decomposition, virtual isolation) and example visualizations (e.g., network level connectivity, brain maps) derived from the original research framework can be discussed upon request. 

