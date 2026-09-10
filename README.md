# CA1 Miniscope Calcium-Imaging Analysis

A self-directed training project using a public mouse CA1 miniscope calcium-imaging dataset to practice a standard neural-population analysis workflow in Python.

[Open the notebook in Google Colab](https://colab.research.google.com/github/mohammadomer49/ca1-miniscope-calcium-analysis/blob/main/notebooks/CA1_Miniscope_Calcium_Imaging_Analysis.ipynb)

## Why this project

I built this small project to gain hands-on familiarity with calcium-imaging analysis using a real public dataset rather than a toy example. The focus is on understanding the workflow, data structure, and interpretation of processed miniscope recordings, not on reproducing the original study or claiming expertise in the acquisition pipeline.

## Dataset

- **Source:** [DANDI Archive, Dandiset 000718](https://dandiarchive.org/dandiset/000718/0.260825.1902)
- **Published version:** `0.260825.1902`
- **Subject:** `Ca-EEG3-4`
- **Session:** Fear Conditioning (`FC`)
- **Brain region:** CA1
- **Modality:** one-photon miniature calcium imaging
- **Processed ROIs:** 783 segmented ROIs
- **Processed calcium sampling rate:** ~14.9 Hz
- **Behavior:** motion estimates, freezing intervals, and three foot-shock events

The NWB file already contains processed optical-physiology outputs. This analysis uses the released denoised and deconvolved traces and does **not** claim to have performed the original motion correction, ROI segmentation, or source extraction.

## Analysis workflow

1. Stream the public NWB file directly from DANDI with `PyNWB` and `remfile`.
2. Inspect the optical-physiology and behavioral modules.
3. Extract denoised and deconvolved calcium activity for 783 ROIs.
4. Z-score ROI activity and visualize representative traces and population activity.
5. Align population activity to the three foot-shock periods.
6. Compare pre-, during-, and post-shock activity descriptively.
7. Convert ezTrack freezing intervals into a mask on the calcium timestamps.
8. Compare freezing and non-freezing epochs at population and ROI levels.
9. Apply PCA to explore low-dimensional population dynamics.

## Selected results

- The three shock events did not show a uniform population-wide response, so the peri-event analysis is treated as descriptive rather than inferential.
- Freezing occupied about 6% of the analyzed session.
- Mean population activity and the fraction of active ROIs differed only slightly between freezing and non-freezing epochs.
- ROI-level responses were heterogeneous, with both increases and decreases during freezing.
- PC1 and PC2 together explained about 9.7% of the population variance, with substantial overlap between freezing and non-freezing states in low-dimensional space.

All figures are generated directly by the notebook when run.

## Tools

Python, NumPy, pandas, Matplotlib, SciPy, scikit-learn, PyNWB, DANDI API, h5py, remfile, Google Colab.

## Reproduce the analysis

```bash
pip install -r requirements.txt
```

Then open `notebooks/CA1_Miniscope_Calcium_Imaging_Analysis.ipynb`. The notebook streams the public NWB file from DANDI, so the raw dataset is not redistributed in this repository.

## Limitations

- One animal and one recording session were analyzed.
- The calcium traces and ROI segmentation were already processed in the public release.
- Deconvolved activity is an inferred event-like representation, not directly recorded spiking.
- Adjacent time points are temporally autocorrelated and are not independent biological replicates.
- Freezing versus non-freezing comparisons are exploratory and descriptive.
- No causal or population-level generalization is claimed.

## License

Code in this repository is released under the MIT License. The source dataset remains subject to the terms and citation requirements of its original DANDI release.
