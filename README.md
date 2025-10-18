# ISI Final Project – NYC Noise Complaints vs Liquor Licenses

## Overview

This project analyzes the correlation between liquor licenses and noise complaints in Brooklyn and Staten Island using NYC Open Data. The analysis focuses on 2024 noise complaints and active liquor licenses to determine if there is a statistically significant relationship between liquor license density and noise complaint frequency by ZIP code.

## Data Sources

This project uses publicly available datasets from NYC Open Data:

1. **NYC 311 Service Requests**
   - URL: https://data.cityofnewyork.us/Social-Services/311-Service-Requests-from-2010-to-Present/erm2-nwe9
   - Description: Contains noise complaints from 2024 filtered for Brooklyn and Staten Island
   - Filter: Complaint Type contains "Noise", Year = 2024, Borough = Brooklyn or Staten Island

2. **NYC Liquor License Data**
   - URL: https://data.cityofnewyork.us/City-Government/Liquor-Authority-Quarterly-List-of-Active-Licenses/tjby-92xf
   - Description: Contains active liquor licenses in Kings County (Brooklyn) and Richmond County (Staten Island)
   - Filter: License Status = Active, County = Kings or Richmond

## Installation

To run this project, you need Python 3.8+ and the following packages:

```bash
pip install pandas numpy matplotlib seaborn jupyter scipy
```

Or install all dependencies at once:

```bash
pip install pandas numpy matplotlib seaborn jupyter scipy
```

## Project Structure

```
ISI-FINAL-PROJECT/
├── notebooks/
│   ├── 01_pipeline.ipynb          # Data loading and cleaning
│   └── 02_merge_analysis.ipynb    # Analysis and visualization
├── data/
│   ├── raw/                        # Raw data files (if downloaded locally)
│   └── clean/                      # Cleaned datasets
│       ├── 311_noise_cleaned.csv
│       └── liquor_cleaned.csv
└── output/                         # Analysis results
    ├── merged_analysis.csv
    ├── liquor_vs_noise_scatter.png
    └── top_10_zip_codes.png
```

## Notebook Workflow

### 1. Data Pipeline (01_pipeline.ipynb)

This notebook handles data acquisition and preprocessing:

- **Load Data**: Fetches data directly from NYC Open Data APIs
- **Filter Data**: 
  - 311 data: Noise complaints in 2024 for Brooklyn and Staten Island
  - Liquor data: Active licenses in Brooklyn and Staten Island
- **Clean ZIP Codes**: Standardizes all ZIP codes to 5-digit format
- **Save Cleaned Data**: Exports to `data/clean/` directory
- **Display Samples**: Shows first few rows for verification

**To run:**
```bash
jupyter notebook notebooks/01_pipeline.ipynb
```

### 2. Merge and Analysis (02_merge_analysis.ipynb)

This notebook performs the correlation analysis:

- **Load Cleaned Data**: Reads from `data/clean/`
- **Group by ZIP Code**: Counts noise complaints and liquor licenses per ZIP
- **Merge Datasets**: Combines counts on ZIP code
- **Calculate Correlation**: Computes Pearson and Spearman correlation coefficients
- **Create Visualizations**: 
  - Scatter plot with trendline showing liquor count vs noise count
  - Bar chart of top 10 most active ZIP codes
- **Save Results**: Exports merged data and charts to `output/` directory

**To run:**
```bash
jupyter notebook notebooks/02_merge_analysis.ipynb
```

## Results

The analysis produces:

1. **Merged Dataset** (`output/merged_analysis.csv`): ZIP code-level counts of noise complaints and liquor licenses
2. **Scatter Plot** (`output/liquor_vs_noise_scatter.png`): Visualization showing the relationship between liquor licenses and noise complaints with a trendline
3. **Top 10 ZIP Codes** (`output/top_10_zip_codes.png`): Bar chart comparing the most active ZIP codes
4. **Statistical Metrics**: Correlation coefficients and p-values indicating the strength and significance of the relationship

## Key Findings

After running the analysis, you will see:
- The correlation coefficient between liquor license density and noise complaints
- Whether the correlation is statistically significant (p-value < 0.05)
- ZIP codes with the highest concentration of both metrics
- Visual representation of the relationship

## Running the Complete Analysis

To run the full analysis from start to finish:

1. Clone this repository
2. Install dependencies (see Installation section)
3. Run the pipeline notebook to load and clean data:
   ```bash
   jupyter notebook notebooks/01_pipeline.ipynb
   ```
   Execute all cells in order
4. Run the analysis notebook to generate results:
   ```bash
   jupyter notebook notebooks/02_merge_analysis.ipynb
   ```
   Execute all cells in order
5. Check the `output/` directory for results

## Notes

- The notebooks load data directly from NYC Open Data APIs, so an internet connection is required
- Large datasets may take several minutes to download
- The API has a limit of 50,000 records per request; if more data is needed, the query may need to be split
- ZIP codes are standardized to 5-digit format; records without valid ZIP codes are excluded from analysis

## License

This project uses public data from NYC Open Data, which is freely available for analysis and research purposes.
