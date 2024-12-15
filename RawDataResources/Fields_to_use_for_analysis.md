# HMDA Data Field Descriptions
## Items marked with (x) are not used in the analysis as features in the model

### HMDA Data Extract Filters Applied 
1. State: Minnesota
2. All Financial Institutions
3. All data fields 

activity_year - Calendar year of data submission (2021-2023) (x) - 3 Years of data 
lei - Legal Entity Identifier for financial institutions (x)
state_code - Two-letter state codeb (MN - static)
county_code - State-county FIPS code (x)
census_tract - 11-digit census tract number 
conforming_loan_limit - Indicates if loan exceeds GSE limits (C/NC/U/NA) (x)
derived_loan_product_type - Combined loan type and lien status 
derived_dwelling_category - Combined construction method and total units (x)
derived_ethnicity - Aggregated ethnicity from applicant/co-applicant (x)
derived_race - Aggregated race from applicant/co-applicant (x)
derived_sex - Aggregated sex from applicant/co-applicant (x)
action_taken - Final status of loan application (1-8) (LABEL) (1 2 and 3)
purchaser_type - Entity purchasing the loan (0-9, 71-72) (x)
preapproval - Whether preapproval was requested (x)
loan_type - Conventional, FHA, VA, or RHS/FSA (1-4) (x)
loan_purpose - Purpose of loan (purchase, refinance, etc.) (x)
lien_status - First or subordinate lien position (x)
reverse_mortgage - Whether loan is a reverse mortgage (x)
open-end_line_of_credit - Whether loan is a line of credit (x)
business_or_commercial_purpose - Whether loan is for business use 
loan_amount - Amount of loan or application (x)
loan_to_value_ratio - Ratio of loan amount to property value (x)
interest_rate - Interest rate of the loan (x)
rate_spread - Difference between APR and APOR (x)
hoepa_status - High-cost mortgage indicator (x)
total_loan_costs - Total loan costs in dollars (x)
total_points_and_fees - Total points and fees charged
origination_charges - Borrower-paid charges at closing
discount_points - Points paid to reduce interest rate
lender_credits - Amount of lender credits
loan_term - Months until loan maturity (x)
prepayment_penalty_term - Months of prepayment penalty
intro_rate_period - Months until first rate change
negative_amortization - Allows negative amortization
interest_only_payment - Allows interest-only payments
balloon_payment - Includes balloon payment
other_nonamortizing_features - Other non-standard payment features
property_value - Value of property (rounded to nearest $10,000) (x)
construction_method - Site-built or manufactured home
occupancy_type - Principal, second home, or investment
manufactured_home_secured_property_type - Home and/or land security
manufactured_home_land_property_interest - Land ownership type
total_units - Number of units in property (1 to >149)
multifamily_affordable_units - Percentage of affordable units
income - Annual gross income in thousands (x)
debt_to_income_ratio - Monthly debt to income ratio (x)
applicant_credit_score_type - Credit score model used 
co-applicant_credit_score_type - Co-applicant credit score model
applicant_ethnicity-1 through -5 - Detailed ethnicity of applicant
co-applicant_ethnicity-1 through -5 - Detailed ethnicity of co-applicant
applicant_ethnicity_observed - Whether ethnicity was visually observed
co-applicant_ethnicity_observed - Whether co-applicant ethnicity was observed
applicant_race-1 - Detailed race of applicant (x)
co-applicant_race-1 through -5 - Detailed race of co-applicant
applicant_race_observed - Whether race was visually observed
co-applicant_race_observed - Whether co-applicant race was observed
applicant_sex - Sex of applicant (x)
co-applicant_sex - Sex of co-applicant
applicant_sex_observed - Whether sex was visually observed
co-applicant_sex_observed - Whether co-applicant sex was observed
applicant_age - Age range of applicant
co-applicant_age - Age range of co-applicant
applicant_age_above_62 - Whether applicant is over 62
co-applicant_age_above_62 - Whether co-applicant is over 62
submission_of_application - Direct or indirect application
initially_payable_to_institution - Whether loan is initially payable to institution
aus-1 through -5 - Automated underwriting systems used
denial_reason-1 - Reasons for application denial (x)
tract_population - Total population in census tract
tract_minority_population_percent - Percentage of minority population (x)
ffiec_msa_md_median_family_income - Median family income for MSA/MD
tract_to_msa_income_percentage - Tract to MSA income percentage
tract_owner_occupied_units - Number of owner-occupied units
tract_one_to_four_family_homes - Number of 1-4 family homes
tract_median_age_of_housing_units - Median age of homes in tract

4. Cleaned Data Fields: (x) - chosen features for analysis (LABEL) - loan approval status

activity_year - Calendar year of data submission (2021-2023) (x) - 3 Years of data 
lei - Legal Entity Identifier for financial institutions (x)
state_code - Two-letter state codeb (MN - static)
county_code - State-county FIPS code (x)
conforming_loan_limit - Indicates if loan exceeds GSE limits (C/NC/U/NA) (x) 
derived_dwelling_category - Combined construction method and total units (x)
derived_ethnicity - Aggregated ethnicity from applicant/co-applicant (x)
derived_race - Aggregated race from applicant/co-applicant (x)
derived_sex - Aggregated sex from applicant/co-applicant (x)
action_taken - Final status of loan application (1-8) (LABEL) (1 2 and 3)
purchaser_type - Entity purchasing the loan (0-9, 71-72) (x)
preapproval - Whether preapproval was requested (x)
loan_type - Conventional, FHA, VA, or RHS/FSA (1-4) (x)
loan_purpose - Purpose of loan (purchase, refinance, etc.) (x)
lien_status - First or subordinate lien position (x)
reverse_mortgage - Whether loan is a reverse mortgage (x)
open-end_line_of_credit - Whether loan is a line of credit (x)
loan_amount - Amount of loan or application (x)
loan_to_value_ratio - Ratio of loan amount to property value (x)
interest_rate - Interest rate of the loan (x)
rate_spread - Difference between APR and APOR (x)
hoepa_status - High-cost mortgage indicator (x)
total_loan_costs - Total loan costs in dollars (x)
loan_term - Months until loan maturity (x)
property_value - Value of property (rounded to nearest $10,000) (x)
income - Annual gross income in thousands (x)
debt_to_income_ratio - Monthly debt to income ratio (x)
applicant_race-1 - Detailed race of applicant (x)
applicant_sex - Sex of applicant (x)
denial_reason-1 - Reasons for application denial (x)
tract_minority_population_percent - Percentage of minority population (x)

5. Data Cleaning 

Cleaned Dataset Info:
RangeIndex: 132242 entries, 0 to 132241
Data columns (total 31 columns):
 #   Column                             Non-Null Count   OriginalDtype  ConvertedDtype Missing Values
---  ------                             --------------   ---------        ---------  -------------
 0   activity_year                      132242 non-null  int64          int64         0
 1   lei                                132242 non-null  object         object        0
 2   state_code                         132242 non-null  object         object        0
 3   county_name                        132242 non-null  object         object        795
 4   conforming_loan_limit              131578 non-null  object         object        664
 5   derived_dwelling_category          132242 non-null  object         object        0
 6   derived_ethnicity                  132242 non-null  object         object        0
 7   derived_race                       132242 non-null  object         object        0
 8   derived_sex                        132242 non-null  object         object        0
 9   action_taken                       132242 non-null  int64          int64         0
 10  purchaser_type                     132242 non-null  int64          int64         0
 11  preapproval                        132242 non-null  int64          int64         0
 12  loan_type                          132242 non-null  int64          int64         0
 13  loan_purpose                       132242 non-null  int64          int64         0
 14  lien_status                        132242 non-null  int64          int64         0
 15  reverse_mortgage                   132242 non-null  int64          int64         0
 16  open-end_line_of_credit            132242 non-null  int64          int64         0
 17  loan_amount                        132242 non-null  float64        float64       0
 18  loan_to_value_ratio                127782 non-null  object         float64       3460
 19  interest_rate                      110042 non-null  object         float64       22390
 20  rate_spread                        104618 non-null  object         float64       27824
 21  hoepa_status                       132242 non-null  int64          int64         0
 22  total_loan_costs                   83792 non-null   object         float64       48450
 23  loan_term                          130713 non-null  object         object        2531
 24  property_value                     130476 non-null  object         float64       3166
 25  income                             127310 non-null  float64        float64       5932
 26  debt_to_income_ratio               129013 non-null  object         object        3229
 27  applicant_race-1                   132231 non-null  float64        int64         111
 28  applicant_sex                      132242 non-null  int64          int64         0
 29  denial_reason-1                    132242 non-null  int64          int64         0
 30  tract_minority_population_percent  132242 non-null  float64        float64       0
dtypes: float64(5), int64(12), object(14)
memory usage: 31.3+ MB

6. Exemptions and Data Collection Notes (FINAL DATA MODEL)

- Small lenders below certain thresholds may be exempt from HMDA reporting requirements
- Business-purpose loans secured by residential property may not require demographic data
- Non-applicable fields may show as "exempt" (e.g. property data for non-dwelling loans)
- Privacy protections allow omission of personal data not critical for underwriting
- HMDA exemptions apply to small-volume lenders and reduced scope reporting fields
- Fields marked "exempt" indicate institution not required to report that data point


Total number of columns: 24
Total count of records: 78,268

Remaining columns and their datatypes:

column name:                        original data type:    converted data type:                                Count of EXEMPT entries:
1. activity_year                          int64                 int64
2. lei                                   object                 object
3. state_code                            object                 object
4. county_name                           object                 object
5. conforming_loan_limit                 object                 object (change descriptive value)
6. derived_dwelling_category             object                 object
7. derived_ethnicity                     object                 object
8. derived_race                          object                 object
9. derived_sex                           object                 object
10. action_taken                           int64                int64 (LABEL)
11. purchaser_type                         int64                object (change descriptive value)
12. preapproval                            int64                object (change descriptive value)
13. loan_type                              int64                object (change descriptive value)
14. loan_purpose                           int64                object (change descriptive value)
15. lien_status                            int64                object (change descriptive value)
16. reverse_mortgage                       int64                object (change descriptive value)
17. open-end_line_of_credit                int64                object (change descriptive value)                     6192 exempt
18. loan_amount                          float64                float64
19. hoepa_status                           int64                object (change descriptive value)
20. income (UOM $1k)                      float64               float64                                     negative income values ????
21. applicant_race-1                     float64                object (change descriptive value)                     10 non-entries
22. applicant_sex                          int64                object (change descriptive value)
23. denial_reason-1                        int64                object (change descriptive value)        420/549 denied application did not have a reason
24. tract_minority_population_percent    float64                float64                                                6192 Exempt 


Total number of remaining columns: 24

After removing columns with 'Exempt' values:
Number of denied applications: 549
Total number of applications: 78,268
Percentage of denied applications: 0.70%

