# Workshop: harmonic regression and complex SVD

This folder contains a complete Python exercise using the young and aged
multi-tissue mouse diurnal RNA-seq data from:

**Wang et al. Redox rhythms promote fitness by modulating ageing-dependent
reprogramming. Nature Metabolism (2026).**

- Article: <https://www.nature.com/articles/s42255-026-01515-x>
- PDF included in this folder: `s42255-026-01515-x.pdf`

## Contents

- `harmonic_regression_csvd_workshop.ipynb`: guided analysis notebook.
- `data/FPKM_JTK.xlsx`: original supplied workbook, including the authors'
  JTK_CYCLE results and FPKM sample columns.
- `data/fpkm_csv/*.csv.gz`: expression-only mirrors used by the notebook.
- `environment.yml`: reproducible Conda environment.
- `s42255-026-01515-x.pdf`: paper associated with the dataset.
- `results/`: created automatically when the notebook is run.

## Learning objectives

1. Fit a 24-hour harmonic regression independently in each tissue and age.
2. Correct gene-level P values with Benjamini-Hochberg correction.
3. Define rhythmic genes using adjustable BH and log2-amplitude thresholds.
4. Compare the number of rhythmic genes in young and aged tissues.
5. Plot cumulative rhythmic-gene counts as a function of amplitude.
6. Construct a complex matrix from cosine and sine coefficients.
7. Run complex SVD using core-clock, pan-rhythmic, or custom gene lists.

## Install Miniconda

Conda is recommended for creating an isolated environment for the workshop.
If Conda is not already installed, download Miniconda for your operating
system from the official page:

<https://docs.conda.io/projects/miniconda/en/latest/>

Follow the installer instructions, then open a new terminal before continuing.

## Create the environment

From this folder:

```bash
conda env create -f environment.yml
conda activate harmonic-csvd
python -m ipykernel install --user --name harmonic-csvd --display-name "Python (harmonic-csvd)"
jupyter lab harmonic_regression_csvd_workshop.ipynb
```

The `ipykernel install` command is needed only once. In JupyterLab, select
**Python (harmonic-csvd)** as the notebook kernel if it is not selected
automatically.

If the environment already exists and `environment.yml` has changed:

```bash
conda env update -f environment.yml --prune
conda activate harmonic-csvd
python -m ipykernel install --user --name harmonic-csvd --display-name "Python (harmonic-csvd)"
```

## Important analysis choices

- Harmonic regression is performed on `log2(FPKM + 1)`.
- The reported amplitude is peak-to-trough harmonic amplitude:
  `2 * sqrt(a^2 + b^2)`.
- BH correction is performed independently within each tissue and age group.
- Six mice were collected per tissue, age, and time point. The samples from
  three mice were pooled before RNA sequencing, producing two RNA-seq samples
  per tissue, age, and time point in the deposited workbook.
- Complex SVD tissue-space magnitudes are mode scaling factors, not direct
  gene-level expression amplitudes.
- The cSVD clock face places ZT0 (lights on) at the top and ZT12 (lights off)
  at the bottom, with ZT increasing clockwise.

## Tissue abbreviations

| Code | Tissue |
|---|---|
| TA | Thoracic aorta |
| AA | Abdominal aorta |
| AR | Aortic arch |
| TH | Tip of heart |
| LH | Left heart |
| RH | Right heart |
| SM | Skeletal muscle |
| LV | Liver |
| BF | Brown fat |
| SP | Spleen |
| WAT | White adipose tissue |
| KD | Kidney |
