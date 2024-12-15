
<div style="box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); border: 1px solid #ddd; padding: 20px; margin: 20px 0;">
    <img src="Readme Graphic.jpg" alt="Project Header Image" style="width: 100%; height: auto;">
</div>

# HMDA Loan Data Analysis and Predictive Modeling Documentation

## Overview
This documentation details the comprehensive data analysis and modeling process for the 2023 Minnesota HMDA (Home Mortgage Disclosure Act) loan application dataset, including data cleaning, exploratory analysis, 
and predictive modeling using KNN classification. For visualization of the data, Tableau was used to create a dashboard and a story the data can be found in the Tableau Workbook File(s).

## Technologies Used
- Python 3.x
- Key Libraries:
  - pandas: Data manipulation and analysis
  - numpy: Numerical operations
  - sklearn: Machine learning utilities and modeling
  - matplotlib: Data visualization
  - seaborn: Statistical data visualization
  - sqlite3: Database management
  - sqlalchemy: Database ORM

## Data Source & Initial Statistics
- Original dataset: `2023_State_MN_HMDA_loan_data(all loan_purpose).csv`
- Initial records: 132,242 entries
- Initial columns: 100 features
- Final records after cleaning: 78,268
- Final features: 24 columns
- Contains comprehensive mortgage application data reported under HMDA requirements

## Data Cleaning Process

### 1. Initial Data Assessment
- Loaded raw data using pandas
- Performed initial analysis of:
  - Dataset information and structure
  - Missing values
  - Basic statistics
  - Data types

### 2. Column Selection
Selected 24 relevant columns including:
- Application details (year, location, loan characteristics)
- Applicant information (race, ethnicity, sex)
- Loan specifics (amount, type, purpose)
- Decision factors (action taken, denial reasons)

### 3. Missing Value Treatment
Systematically removed records with missing values and exempt values in critical fields (did not affect the success of the model):
- Total loan costs
- Rate spread
- Income
- Loan-to-value ratio
- County name
- Conforming loan limit
- Debt-to-income ratio
- Loan term
- Interest rate
- Property value
- Applicant race

### 4. Data Type Standardization
Converted columns to appropriate data types:
- Numeric fields: int64/float64
- Categorical fields: object
- Standardized formats for consistency

### 5. Value Mapping
Mapped numeric codes to descriptive values for better interpretability:
- Conforming loan limit categories
- Purchaser types
- Preapproval status
- Loan types and purposes
- Lien status
- Mortgage characteristics
- Applicant demographics
- Denial reasons

## Final Dataset Characteristics

- Cleaned dataset: `Cleaned_loan_data_for_model.csv`

### Feature Set Details
1. **Temporal Features:**
   - activity_year (int64)

2. **Institutional Information:**
   - lei (object)
   - state_code (object)
   - county_name (object)

3. **Loan Characteristics:**
   - conforming_loan_limit (object)
   - loan_amount (float64)
   - loan_type (object)
   - loan_purpose (object)
   - lien_status (object)
   - reverse_mortgage (object)
   - open-end_line_of_credit (object)
   - hoepa_status (object)

4. **Property Information:**
   - derived_dwelling_category (object)
   - tract_minority_population_percent (float64)

5. **Applicant Demographics:**
   - derived_ethnicity (object)
   - derived_race (object)
   - derived_sex (object)
   - applicant_race-1 (object)
   - applicant_sex (object)

6. **Financial Metrics:**
   - income (float64)
   - purchaser_type (object)
   - preapproval (object)

7. **Decision Information:**
   - action_taken (int64) - TARGET
   - denial_reason-1 (object)

### Data Quality Notes
- Missing Values:
  - 6,192 exempt entries in open-end_line_of_credit
  - 6,192 exempt entries in tract_minority_population_percent
  - 10 non-entries in applicant_race-1
  - 420 out of 549 denied applications lack denial reasons

## Exploratory Data Analysis

### Income Distribution Analysis
- **Box Plot Findings:**
  - Heavily right-skewed income distribution
  - Upper threshold: $276,000
  - Number of outliers: 4,944 (6.3% of total)
  - Outlier Statistics:
    - Minimum: $277,000
    - Median: $367,000
    - Maximum: $1,651,000,000
    - Mean: $900,069
    - Standard Deviation: $23,759,419

### Loan Amount Distribution
- **Box Plot Findings:**
  - Significant right-skewed distribution
  - Multiple extreme outliers above upper whisker
  - Upper threshold: Approximately $750,000
  - Most outliers concentrated in metropolitan areas

### Data Storage and Processing
- **SQLite Database Implementation:**

  - Utilized SQLite for efficient data storage and querying
  - Leveraged SQLAlchemy ORM for database interactions
  - Integrated with pandas for seamless data querying
  - Implemented in Google Colab environment for collaborative analysis
  - Key libraries used: pandas, sqlite3, sqlalchemy

## Machine Learning Implementation

### KNeighbors Classifier Model

#### Data Preprocessing Steps
1. **Handling Exempt Values:**
   - Removed records with exempt status
   - Treated missing denial reasons as separate category

2. **Feature Engineering:**
   - One-hot encoding for categorical variables
   - Standardization of numerical features
   - Target variable: action_taken (binary classification)

3. **Class Imbalance Handling:**
   - Severe imbalance noted (0.70% denial rate)
   - Implementation of class weights

4. **Data Splitting:**
   - Training set: 75% of data
   - Test set: 25% of data
   - Random state: 1 (for reproducibility)

#### Model Variations Tested
1. **KNN with n_neighbors=3:**
   - Initial baseline model
   - Strong performance on majority class
   - Limited performance on minority class

2. **KNN with n_neighbors=5:**
   - Slight improvement in stability
   - Similar overall performance patterns

3. **KNN with n_neighbors=7:**
   - Most balanced performance
   - Better handling of outliers

## Model Performance Considerations

### Class Imbalance Impact
- Extremely skewed dataset (99.30% approvals)
- Need for specialized metrics beyond accuracy
- Focus on recall for denial predictions

### Data Limitations
- High number of exempt entries (6,192 records)
- Missing denial reasons (76.5% of denials)
- Limited demographic variation

### Model Performance Metrics

The KNeighbors Classifier model produced the following performance metrics:

#### Binary Classification Results
- Class 0 (Loan Denials):
  - Precision: 0.77 - Of the loans predicted as denials, 77% were actual denials
  - Recall: 0.34 - The model correctly identified 34% of all actual loan denials
  - F1-Score: 0.48 - Harmonic mean of precision and recall for denials
  - Support: 128 cases in test set

- Class 1 (Loan Approvals):
  - Precision: 1.00 - Nearly perfect precision in identifying approvals
  - Recall: 1.00 - Successfully identified almost all actual approvals
  - F1-Score: 1.00 - Perfect balanced score for approvals
  - Support: 19,439 cases in test set

#### Overall Model Performance
- Accuracy: 1.00 (99.7%) - High overall accuracy driven by majority class
- Macro Average:
  - Precision: 0.88 - Simple average of class precisions
  - Recall: 0.67 - Simple average of class recalls
  - F1-Score: 0.74 - Average balanced performance
- Weighted Average:
  - Precision: 0.99
  - Recall: 1.00
  - F1-Score: 0.99
  - Accounts for class imbalance in calculations

#### Analysis of Results

- The model excels at predicting loan approvals (Class 1)
- Struggles with minority class prediction (denials)
- High precision but low recall for denials indicates:
- Conservative in predicting denials
- Misses many actual denial cases
- Performance metrics heavily influenced by class imbalance
- Model shows signs of overfitting to majority class


## Random Forest Model Performance

### Model Configuration
- Utilized RandomForestClassifier from scikit-learn
- Features standardized using StandardScaler
- Data split into training and test sets
- Focused on binary classification (Approval/Denial)

### Model Performance Metrics

The Random Forest model demonstrated the following performance characteristics:

#### Confusion Matrix Results
                  Predicted 0    Predicted 1
    Actual 0           2            111
    Actual 1           8           15533

#### Binary Classification Results
- Class 0 (Loan Denials):
  - Precision: 0.20 - Of predicted denials, 20% were actual denials
  - Recall: 0.02 - The model correctly identified 2% of actual loan denials
  - F1-Score: 0.03 - Harmonic mean of precision and recall for denials
  - Support: 113 cases in test set

- Class 1 (Loan Approvals):
  - Precision: 0.99 - Near perfect precision in identifying approvals
  - Recall: 1.00 - Successfully identified almost all actual approvals
  - F1-Score: 1.00 - Perfect balanced score for approvals
  - Support: 15,541 cases in test set

#### Overall Model Performance
- Accuracy: 99.24% - High overall accuracy driven by majority class
- Macro Average:
  - Precision: 0.60 - Simple average of class precisions
  - Recall: 0.51 - Simple average of class recalls
  - F1-Score: 0.51 - Average balanced performance
- Weighted Average:
  - Precision: 0.99
  - Recall: 0.99
  - F1-Score: 0.99
  - Accounts for class imbalance in calculations

#### Analysis of Results
- Model shows strong performance on majority class (approvals)
- Significant struggles with minority class prediction (denials)
- Very low recall for denials indicates:
  - Model rarely predicts denials
  - Misses most actual denial cases
- Performance heavily skewed by class imbalance
- Clear signs of majority class bias

#### Model Limitations
- Severe impact of class imbalance
- Poor denial detection capabilities
- Critical need for improvement through:
  - Advanced sampling techniques
  - Class balancing methods
  - Feature engineering
  - Alternative model architectures

## Data Visualization Analysis in Tableau

### 1. County Map Filter (Top Left)

#### Data Source:
- The data for the Tableau dashboard was the same as the data used for the model.
- Financial Institution were identified and merged with the appropiate LEI identifier (performed in Excel using Power Query).
- County names were merged with the appropiate county INCITS codes (performed in Excel using Power Query) - allowed for the creation of a map of the United States.
- Public link to the Tableau dashboard can be found [here](https://public.tableau.com/app/profile/sergei.sergeev/viz/MinnesotaLoanApplicationApprovalHMDAProject4/Dashboard1?publish=yes).

#### Purpose:
- The Tableau dashboard provides a comprehensive analysis of loan applications across counties and their outcomes, 
categorized by loan types and purposes. 
- Allows users to analyze data at a county level by selecting individual counties on the map (heat-map style)

#### Visualization:
- A colored map of counties, highlighting geographic data for loans (allowed for filtering of dashboard data by county)

#### Insight:
- Enables geographic analysis of loan applications across different counties
- Helps pinpoint areas with significant loan activity

### 2. Accepted Application Type Count (Top Right) 
#### Purpose:
- Shows the number of accepted loan applications categorized by Loan Purpose

#### Visualization:
- Bar chart with labels displaying:
  - Count of accepted applications 
  - Corresponding average loan amounts

### Tool Tips Display: 
- Average loan amount for each loan type: full data set
- Average income for each loan type: full data set
- Average loan amount for each loan type (condition: accepted or denied)
- Average income for each loan type (condition: accepted or denied)
- Total number of accepted/denied applications for each loan type

#### Key Observations:
- Home Purchase loans have highest acceptance count (~$311,174.43) - (in both accepted and denied categories)
- Cash-out refinancing and Refinancing show moderate counts but significant loan amounts
- Home improvement and other purposes have fewer accepted applications

### 3. Average Loan Amount Per Loan Type (Bottom Left)
#### Purpose:
- Displays the average loan amount for each Loan Type

#### Visualization:
- Bar chart with labeled loan amounts

#### Key Observations:
- VA Loans (Veterans Affairs guaranteed) show highest average loan amount ($337,806.12)
- Federal Housing Administration (FHA) and Conventional Loans follow closely
- USDA Rural Housing Service loans have lowest average loan amount ($198,372.37)

### 4. Denied Application Loan Type (Bottom Right)
#### Purpose:
- Analyzes count of Denied Applications grouped by Loan Purpose

#### Visualization:
- Bar chart showing:
  - Counts of denied applications
  - Associated loan amounts

#### Key Observations:
- Home Purchase loans show highest number of denials (~$192,391.30)
- Other purpose and Refinancing loans show substantial denials
- Home improvement loans have fewer denials

### Overall Insights

#### Geographic Trends
- Map filter enables regional loan analysis
- Helps identify counties with high loan activities

#### Accepted Applications
- Home Purchase loans dominate acceptance counts
- Indicates strong borrower preference for this purpose

#### Denied Applications
- High denial rates for Home Purchase and Other purpose loans
- Highlights areas requiring further investigation

#### Loan Amount Averages
- VA loans show significantly higher average amounts
- USDA loans remain lower, reflecting target audience differences

### Visualization Impact
The Tableau dashboard effectively analyzes loan application outcomes across multiple dimensions:
- Geographic distribution
- Acceptance and denial patterns
- Loan purpose trends
- Average loan amounts by type

The dynamic county filter provides flexibility for users to examine regional trends, supporting data-driven decision making in loan performance analysis.
This helps us better to understand the loan application process, the dataset used by the k-neighbors classifier model and the factors that affect the loan approval process.

## Future Model Recommendations and Improvements to Consider

### 1. Model Optimization
- Implement class balancing techniques
- Feature selection optimization
- Cross-validation implementation
- Consider ensemble approaches

### 2. Data Pipeline Improvements
- Automated data cleaning process
- Include data from other years to improve the model
- Real-time prediction capabilities
- Model performance monitoring
- Regular retraining schedule

### 3. Business Integration
- API development for model deployment
- User interface for predictions
- Integration with existing systems
- Validation against business rules

### 4. Future Data Collection
- Improve capture of denial reasons
- Reduce exempt entries
- Standardize demographic reporting
- Consider separate models for different loan types

## Output Files
- Cleaned dataset: `Cleaned_loan_data_for_model.csv`
- Model files: `clusters_kneighborsclassifier_model.ipynb`
- Documentation: `README.md`

## Usage
The cleaned dataset and model are ready for:
- Statistical analysis
- Machine learning model development
- Loan approval pattern analysis
- Demographic studies
- Predictive modeling of loan decisions

## Notes
- Regulatory exemptions and reporting requirements considered
- Preserved data integrity while maximizing usability
- Balanced data completeness with sample size
- Maintained audit trail of cleaning steps

## Project Contributors

### Sergei Sergeev
- Role: Project Lead
- Contributions:
  - Data Cleaning
  - Data Cleaning and merging with other data sources for geographic purposes in Tableau
  - Documentation and technical writing

### Sophie Selbure
- Contributions:
  - Exploratory data analysis
  - KNN Model implementation
  - Tableau dashboard development
  - Statistical analysis and reporting

### Maud Rashid
- Contributions:
  - SVM Model implementation
  - Research and analysis of the data
  - Documentation
  - Tableau dashboard development

### Kowsar Abdi
- Contributions:
  - Exploratory data analysis
  - Data visualization
  - Documentation
  - Tableau dashboard development
  - Research and analysis of the data

