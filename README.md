# Analysis Code for: "Persistent Gaps, Partial Gains: A Population-Level Study of COVID-19 Learning Inequalities in the Netherlands"

[![DOI](https://zenodo.org/badge/DOI/[ZENODO-DOI].svg)](https://doi.org/[ZENODO-DOI])

This repository contains the Python analysis code associated with the following publication:

> Alrouh, H., et al. (2026). Persistent Gaps, Partial Gains: A Population-Level Study of COVID-19 Learning Inequalities in the Netherlands. *[JOURNAL NAME]*, [VOLUME]([ISSUE]), [PAGE RANGE]. https://doi.org/[MANUSCRIPT DOI]

---

## Overview

This code reproduces the statistical analyses reported in Persistent Gaps, Partial Gains. The study examines the association between COVID-19 exposure and secondary school examination performance in the Netherlands. Analyses are stratified by educational track -- pre-university education (VWO), senior general secondary education (HAVO), upper pre-vocational education (VMBO-TG), and lower pre-vocational education (VMBO-BK) -- to account for differences in curricular content, examination standards, and student demographics.

For each track, separate generalized linear models (GLM) are estimated with exam score as the outcome. Models include COVID-19 exposure indicators, socio-demographic covariates (gender, migration background, parental education, parental income, and urbanicity), and interaction terms between exposure and each socio-demographic variable to capture differential pandemic effects across subgroups. Categorical variables with more than two levels are dummy-coded; parental education missing values are retained as a separate category; observations with missing values on other variables are excluded.

All analyses were conducted in a secure computing environment provided by Statistics Netherlands (CBS).

---

## Repository Structure

```
.
├── README.md            # This file
├── LICENSE              # MIT License
├── CITATION.cff         # Machine-readable citation metadata
├── requirements.txt     # Python package dependencies
├── tracks.ipynb         # Divides the full sample into 4 tracks
├── CE_vwo_v3.ipynb      # Analysis for Track 1: VWO (pre-university education)
├── CE_havo_v3.ipynb     # Analysis for Track 2: HAVO (senior general secondary education)
├── CE_vmbogt_v3.ipynb   # Analysis for Track 3: VMBO-TG (upper pre-vocational education)
└── CE_vmbobk_v3.ipynb   # Analysis for Track 4: VMBO-BK (lower pre-vocational education)
```

### Script Descriptions

**`tracks.ipynb`**
Reads the full dataset and assigns each observation to one of four subsamples based on the participant's secondary education track: VWO, HAVO, VMBO-TG, or VMBO-BK. Outputs four subsets used as input by the track-specific scripts.

**`CE_vwo_v3.ipynb` (VWO) / `CE_havo_v3.ipynb` (HAVO) / `CE_vmbogt_v3.ipynb` (VMBO-TG) / `CE_vmbobk_v3.ipynb` (VMBO-BK)**
Each script fits a series of generalized linear models (GLM) predicting exam score for the corresponding track subsample. The general model specification is:

```
Exam Score = α + β1·Exposure + β2·SES_variable + β3·(Exposure × SES_variable)
           + β4·Migration + β5·Parental_Education + β6·Parental_Income
           + β7·Urbanicity + ε
```

Separate models are estimated for each socio-demographic dimension of interest (gender, migration background, parental education, parental income). Categorical predictors with more than two levels are dummy-coded. Missing values for parental education are retained as a separate category; observations missing on all other variables are excluded. Outputs include [DESCRIPTION OF OUTPUTS, e.g., "model coefficient tables saved to /output"].

---

## Variables

### Primary Explanatory Variable

**COVID-19 exposure** is operationalized as a set of dummy indicators for examination cohort year. Cohorts 2020, 2021, 2022, and 2023 are treated as exposed, as all experienced pandemic-related disruptions to teaching and assessment. Cohorts 2017, 2018, and 2019 form the pre-pandemic reference group.

### Covariates

**Gender** -- recorded as male or female; included as a binary indicator (male vs. female).

**Migration background** -- follows the CBS classification system, distinguishing between:
- Dutch natives (no migration background) -- reference category
- Second-generation migrants: born in the Netherlands with at least one parent born abroad
- First-generation migrants: born abroad

Both first- and second-generation migrants are further disaggregated into Western and non-Western categories. In CBS terminology, "Western" includes Europe (excluding Turkey), North America, Oceania, Indonesia, and Japan; "non-Western" covers all other countries of origin.

**Parental education** -- measured as the highest qualification attained by either parent, mapped to three levels for international comparability:
- Low: primary education, VMBO (basis/kader streams), and MBO level 1
- Medium: HAVO, VWO, MBO levels 2-4, and HBO or WO bachelor's degrees
- High: HBO or WO master's degrees or doctoral degrees

HBO refers to professionally oriented higher education (universities of applied sciences); WO refers to academic, research-oriented universities. Missing values for parental education are retained as a separate "unknown" category rather than excluded, as missingness is more prevalent among students with a migration background.

**Parental income** -- defined as the average gross income of both parents over the relevant reference year, divided into quintiles to capture relative economic position within the population.

**Urbanicity** -- measured on a five-point ordinal scale representing the degree of urbanization of the student's residential municipality, based on address density as defined by CBS. The scale ranges from 1 (very highly urbanized, ≥ 2,500 addresses per km²) to 5 (very low urbanization, < 500 addresses per km²).

### Interaction Terms

Each model includes interaction terms between the exposure indicators and one focal socio-demographic variable (gender, migration background, parental education, or parental income). These interactions estimate changes in subgroup performance during pandemic-exposed years relative to the pre-pandemic baseline. Because CvTE score normalization is applied uniformly within a given track-year, it does not vary across sociodemographic groups, and the interaction terms are not subject to normalization-induced bias. The main effect of exposure conflates real attainment change with normalization adjustments and should therefore be interpreted with caution.

---

## Requirements

- Python [PYTHON VERSION, e.g., 3.10.x]
- All required packages and their versions are listed in `requirements.txt`

To install dependencies, run:

```bash
pip install -r requirements.txt
```

---

## Data

The analyses were conducted in a secure computing environment provided by Statistics Netherlands (CBS) using microdata not available for public download. Researchers affiliated with a Dutch university or research institution may apply for access to CBS microdata via the [CBS Microdata Services](https://www.cbs.nl/en-gb/our-services/customised-services-microdata/microdata-conducting-your-own-research). Access is subject to CBS terms and conditions.

The specific CBS datasets used in this study are: [DATASET NAMES AND CBS IDENTIFIERS, e.g., "Examination results register (EXAMENUITSLAG), parental income register (INPATAB), etc."].

Because the data cannot be redistributed, the scripts in this repository cannot be run outside of the CBS environment without obtaining equivalent access. The code is shared for transparency and reproducibility documentation purposes.


---

## Reproducibility Note

These scripts are provided as a static record of the analyses reported in the manuscript. They reflect the exact code used at time of publication and are not actively maintained. Note that because the analyses were run inside the CBS secure computing environment, exact reproduction requires both CBS microdata access and an equivalent environment setup. If you have questions about the code or the analytical approach, please open a GitHub issue or contact the corresponding author.

---

## License

This code is released under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Citation

If you use this code in your own work, please cite the original manuscript:

```
Alrouh, H., et al. (2026). Persistent Gaps, Partial Gains: A Population-Level Study of COVID-19 Learning Inequalities in the Netherlands.
[JOURNAL NAME], [VOLUME]([ISSUE]), [PAGE RANGE].
https://doi.org/[MANUSCRIPT DOI]
```


## Authors and Contact

**Hekmat Alrouh** (Corresponding author)
Erasmus University Rotterdam
alrouh@essb.eur.nl

Tom Emery -- Erasmus University Rotterdam
Anja Schreijer -- Erasmus Medical Center
