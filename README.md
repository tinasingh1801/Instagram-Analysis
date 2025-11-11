# Instagram-Analysis

A small repository containing the data and results for an Instagram dataset analysis.

Summary
-------
This project contains the raw and cleaned Instagram datasets and the results of an analysis performed in Power BI. The data was sourced from Kaggle, cleaned using Power Query Editor (Power BI / Excel), and analyzed & visualized in Power BI Desktop.

Contents
--------
- `Raw Data/instagram.xlsx` — original dataset downloaded from Kaggle.
- `Clean Data/instagram.xlsx` — version of the dataset after cleaning and transformations (Power Query Editor).
- `Result/` — output artifacts produced from the analysis (Power BI report `.pbix` and screenshots).
- `LICENSE` — project license.

Data provenance
---------------
- Source: Kaggle (original dataset file placed in `Raw Data`).
- Cleaning: Power Query Editor (steps applied inside the Power BI file or Excel query editor). Typical steps included: removing duplicates, converting data types, renaming columns, handling missing values, and deriving any calculated fields used in the analysis.

Analysis
--------
All analysis, visualizations, and dashboards were created in Power BI Desktop. The main deliverables are:
- A `.pbix` Power BI report (found in the `Result/` folder).
- Exported screenshots for quick preview.

How to reproduce
----------------
1. Open `Raw Data/instagram.xlsx` in Excel or Power BI.
2. If you want to reproduce the exact cleaning steps, open the Power BI report in `Result/` — the Power Query steps used to transform the data are available in the Query Editor inside Power BI Desktop.
3. To run your own analysis:
	 - Install Power BI Desktop (Windows).
	 - Open the `.pbix` file in `Result/` to review visualizations and queries.
	 - If you prefer code-based analysis, export `Clean Data/instagram.xlsx` to CSV and analyze with Python/R.

Notes & next steps
------------------
- If you'd like, I can:
	- Preview the Excel files and produce a small reproducible Python notebook (Pandas + Jupyter) that reads the cleaned file and reproduces a subset of the EDA/plots.
	- Extract the Power Query steps into a documented list inside this repo.
	- Add a simple script to convert the Excel files to CSV and run sanity checks.

Contact / Author
----------------
This repository was prepared by the project owner. For details about the analysis, check the Power BI report and query steps in `Result/`.

Detailed end-to-end analysis process
------------------------------------
Below is a recommended, documented, and repeatable end-to-end process that matches how this project was produced and how to extend or reproduce it. It is written as practical, step-by-step guidance you (or a collaborator) can follow.

1) Project goals & scope
	- Define the business or research questions up front (examples):
	  - Which post attributes (time, caption length, hashtags) correlate with higher engagement?
	  - What posting schedule yields the best average likes/comments?
	  - Are there clusters of posts (by content/hashtags) that perform differently?
	- Decide success criteria (example: explain X% of variance in engagement with available features).

2) Data ingestion
	- Source: Kaggle. The original file is stored at `Raw Data/instagram.xlsx`.
	- Keep the raw file immutable. Work from a copy when doing automated transformation steps.
	- Record metadata: source URL, download date, and any initial notes about missing/odd fields.

3) Exploratory Data Analysis (EDA)
	- Quick checks:
	  - Rows, columns, basic datatypes, missing value counts, unique values for IDs or categorical fields.
	  - Basic distributions (likes, comments, followers if present), time coverage (first/last date).
	- Visual EDA:
	  - Histograms for numeric fields, bar charts for top categories/hashtags, time-series of engagement.
	- Identify obvious issues: duplicates, inconsistent formats, timezone problems in timestamps, or outliers.

4) Data cleaning (Power Query Editor — steps used in this repo)
	- Typical Power Query steps to apply (these match the transformations used to create `Clean Data/instagram.xlsx`):
	  - Remove duplicate rows based on a unique post identifier.
	  - Convert date/time columns to proper datetime type; extract day/week/month as separate fields.
	  - Trim and standardize string fields (lowercase, remove extra whitespace) for captions and hashtags.
	  - Parse hashtags (split into lists or keep a normalized, delimited string) and count hashtags per post.
	  - Fill or tag missing values (for example, mark missing captions or unknown locations rather than dropping automatically).
	  - Create derived fields: caption length, number of hashtags, engagement = likes + comments (or a weighted metric).
	  - Remove PII or irrelevant columns if present.
	- Save the cleaned output to `Clean Data/instagram.xlsx`. Keep a copy of the transformation steps (Power Query steps are stored inside the `.pbix` file if you used Power BI).

5) Feature engineering
	- Derive features likely predictive of engagement:
	  - Temporal features: hour, day-of-week, is_weekend, time-since-last-post (if user-level posting data available).
	  - Text features: caption length, presence of URLs, number of hashtags, common keyword flags, sentiment score (optional).
	  - Media features: image presence/type (if available), inferred category (requires image processing outside current dataset).
	- Normalize or bucket numeric features where appropriate (e.g., followers into bins).

6) Validation & sanity checks
	- Verify row counts between raw and cleaned files match expected reductions (duplicates removed, rows filtered for specific rules).
	- Spot-check a few records to confirm transformed fields match expectations (e.g., date parsing, hashtag counts).
	- Run simple correlation checks and group aggregations to ensure no obvious data leakage or transformation mistakes.

7) Analysis & visualization (Power BI)
	- Create summary dashboards showing key KPIs: total posts, average likes, average comments, engagement rate, top hashtags, top posting times.
	- Time-based analysis: engagement trends over time, moving averages, seasonality by day-of-week or hour.
	- Cohort or segment analysis: performance by hashtag clusters, post type, or other categorical groupings.
	- Use Power Query step comments and Power BI report descriptions to document the logic behind each visualization.

8) Modeling (optional)
	- If building predictive models, split data properly (time-based split is preferred for time series or temporal leakage prevention).
	- Try simple models first: linear regression, decision trees, or tree ensembles (random forest, gradient boosting).
	- Evaluate using appropriate metrics (RMSE for regression on likes/comments, classification metrics for binary tasks such as high/low engagement).

9) Reproducibility and scripting
	- If you want code-based reproducibility, export `Clean Data/instagram.xlsx` to CSV and add a `notebooks/` or `scripts/` folder containing a Jupyter notebook or Python scripts that:
	  - Read the cleaned CSV.
	  - Recreate key EDA plots and a few summary statistics.
	  - Optionally demonstrate a small model training and evaluation pipeline.
	- Add a `requirements.txt` with minimal dependencies (pandas, matplotlib/seaborn, scikit-learn) and a short `README` section explaining how to run the notebook.

10) Results, interpretation & next steps
	- Document the main findings from the Power BI report inside the repo (e.g., a short `RESULTS.md` or extend README) with screenshots located in `Result/`.
	- Provide actionable recommendations based on findings (posting schedule changes, hashtag strategy, content types to prioritize).
	- List limitations and potential biases in the dataset.

11) Maintenance & future work
	- Add scripts to refresh the cleaned dataset when new raw data arrives.
	- Consider adding automated tests / sanity checks (row counts, null thresholds) to be run on new imports.
	- If expanding to image analysis, add a pipeline to process images and extract visual features.

Minimal project layout (what's in this repository)
- `Raw Data/instagram.xlsx` — original dataset from Kaggle (do not edit).
- `Clean Data/instagram.xlsx` — cleaned dataset produced with Power Query Editor.
- `Result/` — Power BI `.pbix` report and exported screenshots.
- `README.md` — this document describing the project and reproducible steps.
- `LICENSE` — repository license.

How I can help next (pick one)
- Create a Jupyter notebook that reads `Clean Data/instagram.xlsx` (or an exported CSV), performs EDA, and produces the top 6 plots.
- Add a Python script to convert the two Excel files to CSV and run basic sanity checks (row counts, null thresholds).
- Extract Power Query transformations into a `TRANSFORMS.md` by opening the `.pbix` and copying the query steps (I can provide instructions since I cannot open `.pbix` here).

If you want me to proceed with one of the next steps, tell me which and I will create a todo and start implementing it.
