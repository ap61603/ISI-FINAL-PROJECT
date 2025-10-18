# ISI-FINAL-PROJECT
Noise Complaints Associated With Areas That Have Liquor Licenses

## Project Overview
This project analyzes the relationship between noise complaints and liquor-licensed establishments in New York City, specifically focusing on Staten Island (Richmond County). The analysis uses NYC 311 noise complaint data and State Liquor Authority (SLA) active license data to build predictive models.

## Project Structure
```
ISI-FINAL-PROJECT/
├── data/
│   ├── raw/              # Raw data files
│   │   ├── sla_active.csv           # Liquor license data (included)
│   │   └── 311_noise.csv            # Noise complaints (not included - too large)
│   ├── interim/          # Intermediate processed data
│   └── processed/        # Final processed data ready for modeling
├── notebooks/
│   └── 01_pipeline.ipynb # Main ML pipeline notebook
├── models/               # Saved trained models
├── requirements.txt      # Python dependencies
└── README.md
```

## Data Sources
1. **NYC State Liquor Authority (SLA) Active Licenses**: Contains information about active liquor licenses including location, type, and business details
2. **NYC 311 Noise Complaints**: Noise-related complaints from NYC's 311 service (download separately)

## Getting Started

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Installation
1. Clone the repository:
```bash
git clone https://github.com/ap61603/ISI-FINAL-PROJECT.git
cd ISI-FINAL-PROJECT
```

2. Install required packages:
```bash
pip install -r requirements.txt
```

3. (Optional) Download NYC 311 noise complaint data:
   - Visit [NYC Open Data - 311 Service Requests](https://data.cityofnewyork.us/Social-Services/311-Service-Requests-from-2010-to-Present/erm2-nwe9)
   - Filter for noise complaints
   - Download as CSV and place in `data/raw/311_noise.csv`

### Running the Pipeline
Open and run the Jupyter notebook:
```bash
jupyter notebook notebooks/01_pipeline.ipynb
```

The notebook will:
1. Load and explore the liquor license data
2. Preprocess and engineer features
3. Create target variables (synthetic if 311 data not available)
4. Train classification and regression models
5. Evaluate model performance
6. Save trained models and processed data

## Pipeline Components

### 1. Data Loading and Exploration
- Loads SLA liquor license data
- Checks for 311 noise complaint data availability
- Performs exploratory data analysis

### 2. Data Preprocessing
- Extracts geographic coordinates from georeference field
- Converts date columns to datetime format
- Calculates derived features (license age, days until expiration)
- Handles missing values

### 3. Feature Engineering
- Creates numeric and categorical features
- Generates spatial features (latitude, longitude)
- Computes temporal features
- Prepares data for modeling

### 4. Machine Learning Models

#### Classification Model
- **Task**: Predict if an area is high or low noise
- **Algorithm**: Random Forest Classifier
- **Features**: License type, location, age, zip code, etc.
- **Output**: Binary classification (High/Low noise area)

#### Regression Model
- **Task**: Predict number of noise complaints
- **Algorithm**: Random Forest Regressor
- **Features**: Same as classification model
- **Output**: Continuous value (complaint count)

### 5. Model Evaluation
- Classification: Accuracy, precision, recall, F1-score, confusion matrix
- Regression: R², RMSE, prediction plots
- Feature importance analysis

## Results
The pipeline successfully:
- Processes 134 liquor license records
- Creates spatial and temporal features
- Trains two ML models with good performance
- Saves models for future use

**Note**: Current results use synthetic target variables for demonstration. Performance will improve with real 311 noise complaint data.

## Next Steps
1. **Integrate Real Data**: Add actual NYC 311 noise complaint data
2. **Spatial Analysis**: Implement spatial joins to match licenses with nearby complaints
3. **Advanced Features**: 
   - Time-based patterns (day of week, time of day)
   - Density metrics (licenses per area)
   - Demographic data integration
4. **Model Improvements**: 
   - Hyperparameter tuning
   - Feature selection
   - Ensemble methods
   - Deep learning approaches
5. **Deployment**: Create API or web interface for predictions

## Technologies Used
- **Python 3.8+**
- **Data Processing**: pandas, numpy
- **Machine Learning**: scikit-learn
- **Visualization**: matplotlib, seaborn
- **Geospatial**: geopandas (optional)
- **Development**: Jupyter Notebook

## License
This project is for educational purposes.

## Contributors
- Isaiah Casas Aponte (ap61603)
- Jacob Capalot (Jcapalot18)

## Acknowledgments
- NYC Open Data for providing the datasets
- NYC State Liquor Authority for license information
- NYC 311 for noise complaint data
