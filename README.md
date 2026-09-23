# Olympic History Analysis

A reproducible, notebook-first exploration of athlete participation, medals, and NOC representation in the modern Olympic Games. The analysis lives in [`olympic_history_analysis.ipynb`](olympic_history_analysis.ipynb); it uses pandas for calculation and matplotlib/seaborn for charts. It is descriptive historical analysis, with no forecasting model.

## Analysis guide

The notebook inspects schema, exact duplicates, missing values, and observed Games before analysis. It then:

- ranks the top five NOCs by distinct athlete `ID` at the first and last observed Games, overall and separately for Summer and Winter;
- charts annual participation for each endpoint's top-five group;
- finds all athletes tied for the most gold and total medal awards;
- counts distinct athletes whose NOC differs from their immediately previous Olympic appearance;
- finds every sport tied for the fewest distinct medal-winning athletes;
- charts participation by season and recorded sex, plus the number of sports and events.

The source covers Athens 1896 through Rio 2016. `athlete_events.csv` has **one row per athlete-event**, so raw row counts are not athlete counts. Counts of people use unique `ID` values. Medal records count one award per athlete, Games, and Event, including each recorded team member's award. NOC codes drive team comparisons; `noc_regions.csv` supplies display labels, which can be imperfect for historical delegations. Missing demographic fields do not cause otherwise valid athlete-event rows to be dropped. The notebook uses observed Games rather than assuming a regular schedule: some Games were cancelled, Summer and Winter coincided through 1992, and they were staggered afterward. Trends are descriptive and do not establish causes.

## Data setup

1. Download the Kaggle dataset [**120 years of Olympic history: athletes and results**](https://www.kaggle.com/datasets/heesoo37/120-years-of-olympic-history-athletes-and-results) yourself. No Kaggle credentials are needed by this project.
2. Extract these two files into `data/`, keeping their names exactly:
   - `data/athlete_events.csv`
   - `data/noc_regions.csv`
3. Keep the CSVs locally. `.gitignore` excludes them from version control; `data/.gitkeep` preserves the empty directory in the repository.

The notebook checks for **both** files before loading. If either is absent, it raises a `FileNotFoundError` listing each missing path and telling you where to put it. It never downloads data or asks for API credentials.

## Install and run

Use Python 3.10 or newer. From the repository root, create an environment:

```bash
python -m venv .venv
```

Activate it with `.venv\Scripts\Activate.ps1` in PowerShell or `source .venv/bin/activate` in macOS/Linux shells. Then install and launch the notebook:

```bash
python -m pip install -r requirements.txt
python -m notebook olympic_history_analysis.ipynb
```

In Jupyter, select that environment's Python kernel and choose **Run All**. The notebook uses `Path.cwd() / "data"`, so launch Jupyter from the repository root. All tables, findings, and charts are calculated when the CSVs are present; the committed notebook contains no fabricated outputs.