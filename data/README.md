# Data

This project uses the **Student Performance Factors** dataset from Kaggle:
https://www.kaggle.com/datasets/ayeshasiddiqa123/student-performance

The raw file (`StudentPerformanceFactors.csv`) is not committed to this repository (see `.gitignore`) since it is third-party data. To reproduce the analysis:

1. Download `StudentPerformanceFactors.csv` from the Kaggle link above.
2. Place it in this `data/` folder.
3. Run the notebook in `notebooks/data_cleaning_and_descriptive_stats.ipynb` from the top.

## Shape

- **Raw**: 6,607 rows x 20 columns
- **Cleaned**: 6,606 rows x 12 columns (11 retained + 1 calculated: `Score_Improvement`)

See the main [README](../README.md) for the full list of columns dropped and why.
