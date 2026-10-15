# Exercise Experience and Calories Burned per Hour

I used R to compare calories burned per hour between novice and experienced male exercisers in the Gym Members Exercise Dataset. I used a permutation test, bootstrap confidence interval, and Welch two-sample t-test to examine the difference and its uncertainty.

**[View the HTML report](https://kadinkolstad.github.io/exercise-experience-analysis/exercise_experience_analysis.html)**

## Research question

Is there a difference in mean calories burned per hour between male records with experience levels 1 and 3 in this dataset?

I calculated calories per hour by dividing `Calories_Burned` by `Session_Duration (hours)`. This accounts for session duration when comparing recorded calorie expenditure; it does not directly measure workout quality, fitness, or training progress.

## Main results

| Group | Records | Mean calories per hour | Standard deviation |
| --- | ---: | ---: | ---: |
| Novice: experience level 1 | 197 | 755.43 | 84.66 |
| Experienced: experience level 3 | 101 | 759.30 | 79.02 |

The observed mean difference was **3.87 calories per hour**, calculated as experienced minus novice.

| Method | Result |
| --- | --- |
| Permutation test: 10,000 shuffles | p-value = 0.7058 |
| Bootstrap: 10,000 resamples within each group | 95% percentile interval: -15.63 to 23.17 calories/hour |
| Welch two-sample t-test | p-value = 0.6965; 95% interval: -15.66 to 23.40 calories/hour |

I did not find strong evidence of a difference between the two groups. Both confidence intervals include zero. This does not establish that the groups are equivalent.

## Data source

- **Dataset:** [Gym Members Exercise Dataset](https://www.kaggle.com/datasets/valakhorasani/gym-members-exercise-dataset)
- **Creator:** Vala Khorasani
- **License listed on Kaggle:** Apache 2.0
- **CSV used in this analysis:** 973 rows and 15 columns

The data checks found no missing values, duplicate full rows, or nonpositive session durations. These checks do not establish that records represent unique individuals or that the sample is representative.

The CSV is downloaded separately from Kaggle. Save it as `exercise_tracking.csv` in the same folder as the R Markdown file. The original data-collection and sampling methods have not been verified for this project.

## Methods

1. Checked the dataset and explored the selected variables.
2. Restricted the main comparison to records labeled Male with experience level 1 or 3.
3. Calculated calories burned per hour and summarized the groups.
4. Shuffled group membership 10,000 times to assess the observed mean difference.
5. Resampled each group separately 10,000 times to estimate bootstrap uncertainty.
6. Compared the bootstrap percentile interval with the Welch confidence interval.

The analysis uses `set.seed(42)` before resampling. The reported values above come from the included knitted HTML.

## Files

| File | Purpose |
| --- | --- |
| `exercise_experience_analysis.Rmd` | R code and written analysis |
| `exercise_experience_analysis.html` | Knitted report with saved results and embedded charts |
| `README.md` | Project overview, results, data source, and running instructions |
| `.gitignore` | Excludes local R session and editor files |

## Run locally

1. Install R and RStudio.
2. Download or clone this repository and extract it if necessary.
3. Download the CSV from the Kaggle source above. Name it `exercise_tracking.csv` and place it alongside `exercise_experience_analysis.Rmd`.
4. Install the required R packages once:

   ```r
   install.packages(c("tidyverse", "rmarkdown"))
   ```

5. Open `exercise_experience_analysis.Rmd` in RStudio, restart the R session, and select **Knit to HTML**.

The existing HTML can be viewed without running R. To reproduce the calculations, use the R Markdown file and the source CSV. Package versions are not pinned.

## Limitations

- The original collection process, sampling method, and independence of records have not been verified.
- The comparison covers only male records in experience levels 1 and 3.
- The analysis does not adjust for workout type, body weight, age, or other potential differences between groups.
- The tests treat records as independent; the permutation test assumes exchangeable group labels under its null hypothesis.
- The results do not establish causation or equivalence between groups.

I would treat this project as an application of statistical comparison and resampling methods rather than a general conclusion about exercise experience.
