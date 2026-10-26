\# Proximal Outcome Drift: How Research on Immersive Health-Professions Training Defines Success



Code, data and figures for a class paper in \*\*Computational Theory Construction\*\* (University of Arkansas, Fall 2026).



The project analyzes 3,905 bibliographic records on immersive technology (VR/AR/MR) in health-professions

education. It uses topic modeling and dictionary-based text analysis to examine how this research measures

success, and builds a theory from the resulting patterns: \*\*proximal outcome drift\*\*.



\*\*Author:\*\* Farzana Fahmee, University of Arkansas (ffahmee@uark.edu)



> This repository is private because the data files contain article abstracts, which are copyrighted by

> their publishers. Please do not redistribute the data files.



\---



\## Repository contents



\### Notebooks (run in this order)



| Step | Notebook | What it does |

|---|---|---|

| A | `bibliography\_cleaning.ipynb` | Cleans and screens the 5,000 exported records: flags duplicates, unusable descriptions and off-scope records |

| B | `topic\_modeling.ipynb` | Removes non-English records (final N = 3,905), fits the TF-IDF + NMF topic model (10 topics), labels topics, and produces the word-frequency, topic and sentiment outputs |

| C | `pattern\_surfacing\_steps.ipynb` | Extracts publication years, builds outcome and design-feature indicators, compares topics and periods, runs the within-topic check and logistic regressions, compares hand coding with dictionary codes, and produces the paper's figures |

| — | `bibliography\_full\_backup.ipynb` | Earlier working copy that combines cleaning with early topic and sentiment steps. Kept for the record; \*\*not needed\*\* to reproduce the results |



\### Folders



| Folder | Contents |

|---|---|

| `data/` | Raw export, cleaned files, topic assignments, result tables and the hand-coding sheet |

| `figures/` | All figures |



\### Data files



| File | Created by | Description |

|---|---|---|

| `OneSearchBib\_data.csv` | Library export | Raw export of 5,000 records (starting point) |

| `bibliography\_working.csv` | Step A | All 5,000 records with cleaning and screening flags |

| `bibliography\_provisional\_core.csv` | Step A | Records provisionally kept during screening |

| `bibliography\_scope\_review.csv` | Step A | Records set aside for manual scope review |

| `repeated\_titles\_review.csv` | Step A | Records sharing a title, checked as possible duplicates |

| `bibliography\_final\_analysis.csv` | Step A | 3,932 records kept after screening |

| `bibliography\_model\_input.csv` | Steps A–B | Topic-model input before removing non-English records |

| `cleaning\_summary.csv` | Step A | Counts of records by screening status |

| `topic\_assignments\_draft.csv` | Step B | 3,905 records with their assigned topic (input to Step C) |

| `topic\_labels\_draft.csv` | Step B | Topic numbers, paper counts and provisional labels |

| `overlapping\_topic\_counts.csv` | Step B | Records per topic under a 25% topic-weight threshold |

| `sentiment\_scores\_exploratory.csv`, `tone\_by\_topic.csv` | Step B | Exploratory sentiment check (not used for the paper's claims) |

| `pattern\_evidence\_papers.csv`, `mechanism\_evidence\_papers.csv` | Step B | Papers selected for close reading |

| `step1\_papers\_with\_year.csv` to `step6\_regression\_results.csv` | Step C | Year extraction, indicator flags, topic and period comparisons, within-topic check, regression results |

| `step8\_hand\_check\_sheet.xlsx` | Step C + manual coding | \*\*The author's manual codes\*\* for 60 randomly sampled abstracts |

| `step8\_hand\_check\_sheet.csv` | Step C | Blank coding sheet created by Step 8 (no codes) |

| `step8\_computer\_answers.csv` | Step C | Dictionary codes for the same 60 abstracts |

| `step9\_validation\_results.csv` | Step C | Agreement between manual and dictionary codes |



\---



\## Data source



Records were exported from the University of Arkansas \*\*OneSearch\*\* library database on \*\*August 31, 2026\*\*.



\- \*\*Search:\*\* terms for immersive technology (virtual, augmented, mixed and extended reality) combined with

&#x20; terms for health-professions education and training (medicine, nursing, surgery, dentistry, pharmacy,

&#x20; clinical education)

\- \*\*Filters:\*\* peer-reviewed; published 2001–2026

\- \*\*Results:\*\* 8,323 matching records; the platform's export limit allowed 5,000 to be downloaded



\---



\## How to reproduce the results



\### 1. Install the software



Install \[Anaconda](https://www.anaconda.com/download) (Python 3). Then open \*\*Anaconda Prompt\*\* (Windows) or

\*\*Terminal\*\* (Mac), go to the repository folder, and run:



```

pip install -r requirements.txt

```



\### 2. Put the data files next to the notebooks



The notebooks read and save files in their own folder. Before running, \*\*copy all files from `data/` into

the main repository folder\*\*, the same folder as the notebooks.



\### 3. Run the notebooks in order



Open \*\*Jupyter\*\* from Anaconda Navigator, open each notebook, and run every cell from top to bottom

(Shift + Enter):



1\. `bibliography\_cleaning.ipynb`

2\. `topic\_modeling.ipynb`

3\. `pattern\_surfacing\_steps.ipynb`



Each notebook saves files that the next one reads, so the order matters.



> \*\*Note on Steps 8 and 9:\*\* Step 8 creates a blank coding sheet (`step8\_hand\_check\_sheet.csv`).

> Step 9 compares the dictionary codes with the \*\*manual codes in `step8\_hand\_check\_sheet.xlsx`\*\*, which

> rerunning Step 8 does not overwrite. Keep the provided `.xlsx` file to reproduce the reported agreement.



\### 4. Check your results



If everything ran correctly, you should get these values:



| Check | Expected value |

|---|---|

| Records after screening | 3,932 |

| Final analysis corpus (English) | 3,905 |

| Papers by period (2001–12 / 2013–18 / 2019–22 / 2023–26) | 222 / 336 / 900 / 2,447 |

| Largest topic (instructional comparisons and learning outcomes) | 675 papers |

| Abstracts mentioning engagement or confidence, 2001–12 → 2023–26 | 6.3% → 37.1% |

| Abstracts mentioning transfer to practice, 2001–12 → 2023–26 | 18.9% → 8.3% |

| Odds ratio per 5 years, engagement/confidence (topic fixed effects) | 2.11 (95% CI 1.84–2.41) |

| Odds ratio per 5 years, transfer to practice | 0.84 (95% CI 0.76–0.93) |

| Manual vs. dictionary agreement (60 abstracts) | 77%–80% |



\---



\## Settings that make the results repeatable



| Setting | Value |

|---|---|

| Text weighting | TF-IDF, single words and two-word phrases, `min\_df=10`, `max\_df=0.80`, `max\_features=12000` |

| Topic model | NMF, 10 topics, `init="nndsvda"`, `random\_state=42`, `max\_iter=400` |

| Topic overlap threshold | 25% of a record's topic weight |

| Time periods | 2001–2012, 2013–2018, 2019–2022, 2023–2026 |

| Within-topic comparison | 2019 and earlier vs. 2023 and later; topics with at least 10 early papers |

| Regression | Logistic regression with topic fixed effects; year in five-year units centered on 2020 |

| Hand-coding sample | 60 abstracts, `random\_state=2026` |



\---



\## Figures



| Figure in paper | File | Made in |

|---|---|---|

| Figure 1: Analysis workflow | `fig0\_workflow.png` | Step C |

| Figure 2: Corpus selection | `fig1\_corpus\_flow.png` | Step C |

| Figure 3: Research streams over time | `fig2\_stream\_shift.png` | Step C |

| Figure 4: Two evaluation clusters | `fig3\_evidence\_regimes.png` | Step C |

| Figure 5: Two design logics | `fig\_two\_logics.png` | Step C |

| Figure 6: Outcome drift over time | `fig4\_outcome\_drift.png` | Step C |

| Figure 7: Change within topics | `fig5\_within\_topic\_drift.png` | Step C |

| Figure 8: Theory model | `fig\_theory\_model.png` | Step C |

| Appendix A1: Word frequencies | `word\_cloud.png` | Step B |

| Appendix A2: Topic overlap | `overlapping\_topics.png` | Step B |

| Not in paper (same counts as Table 1) | `topic\_distribution.png` | Step B |



\---



\## Notes and limitations



\- \*\*Screening decisions:\*\* some screening decisions were made by hand during cleaning. They are saved as flags

&#x20; in `bibliography\_working.csv`, so the later steps reproduce them exactly.

\- \*\*Manual coding:\*\* the 60 manual codes were assigned by the author using written decision rules (see the

&#x20; paper's Methods section), with an AI assistant as second reviewer and final decisions made by the author.

\- What the indicators measure dictionary indicators capture how abstracts \*describe\* evaluation, not

&#x20; verified study designs. Agreement with manual coding was 77%–80%.

\- \*\*Coverage:\*\* the export cap means the corpus covers 5,000 of 8,323 matching records.



\---



\## Citation



Fahmee, F. (2026). Proximal outcome drift: How research on immersive health-professions training defines

success \[Unpublished class paper]. University of Arkansas.

