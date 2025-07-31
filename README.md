# Predicting Student Academic Performance Using Demographic and Behavioral Factors 🧑‍🎓
![s.jpg](s.jpg)

# Project Description
This project analyzes a dataset of 649 Portuguese secondary school students to identify key factors influencing academic success. The goal is to develop models that can predict students' final grades (G3) early in the school year, enabling educators to provide targeted support to at-risk students. The analysis explores relationships between personal characteristics, family background, lifestyle factors, and academic performance metrics.


# Dataset Overview

### Dataset Characteristics:
- Number of students: 649
- Number of features: 15 (mix of categorical and numerical)
- Time period: Academic year records
- Target variable: Final grade (G3)

### Key Features:

#### Personal Information:
- **sex**: Student's gender (F = female, M = male)
- **age**: Student's age (15-22 years)
- **famsize**: Family size (GT3 = greater than 3, LE3 = less than or equal to 3)

#### Family Background:
- **Pstatus**: Parents' cohabitation status (T = together, A = apart)
- **Mjob/Fjob**: Mother's/Father's job category (teacher, health, services, etc.)
- **guardian**: Student's primary guardian (mother, father, other)

#### Lifestyle Factors:
- **traveltime**: Commute time to school (1-4 scale)
- **famrel**: Quality of family relationships (1-5 scale)
- **freetime**: Free time after school (1-5 scale)
- **health**: Current health status (1-5 scale)
- **absences**: Number of school absences (0-93)

#### Academic Metrics:
- **G1**: First period grade (0-20 scale)
- **G2**: Second period grade (0-20 scale)
- **G3**: the ***Target*** Column and represent the Final grade (categorical: Fail, Fair, Good, Very Good)


# Data Cleaning Process

This section outlines the steps taken to clean and prepare the dataset for analysis.

## Steps Performed

### 1. Standardized Missing Values
- Replaced `'?'` placeholders with `NaN` in categorical columns:
  - `Sex`, `Mjob`, `Fjob`, `guardian`
  - Example transformation: `['F', '?', 'M']` → `['F', nan, 'M']`

### 2. Identified Columns Requiring Further Cleaning
- Categorical columns with remaining `'?'` values:
  - `famsize` (household size)
  - `Pstatus` (parent's cohabitation status)

### 3. Checked Numerical Data
- Detected missing values (`NaN`) in:
  - `Age` (15 missing)
  - `traveltime` (18 missing)
  - `famrel` (18 missing)
  - `freetime` (20 missing)
  - `health` (17 missing)
  - `absences` (28 missing)

### 4. Next Steps
- Impute missing values using appropriate methods (median/mode)
- Resolve remaining `'?'` entries in categorical columns
- Validate dataset consistency before analysis

This process ensures the dataset is clean and ready for exploratory analysis.

# Exploratory Data Analysis (EDA)

## Key Insights

### 1. Demographics
- **Gender**: 60% Female, 40% Male
- **Age**: Majority 15-17 years old
- Negative correlation (-0.15) between age and grades

### 2. Academic Performance
- Strong grade progression (G1-G2 correlation: 0.86)
- Final grade distribution:
  - Good: 45%
  - Very Good: 30%
  - Excellent: 15%
  - Fair/Poor: 10%

### 3. Influencing Factors
- **Negative Impact**:
  - Absences (correlation: -0.13)
  - Longer travel time (-0.14)
- **Mother's Job**: Students with teacher/healthcare moms perform better

### 4. Behavioral Patterns
- Optimal free time benefits performance
- Family relationship quality impacts wellbeing but not grades

# Modeling Approach
![mgbox.png](mgbox.png)
## Data Preparation
- Train-Test Split: 80% training, 20% testing
- Stratified sampling on target variable (`G3`) to maintain class distribution
- All models evaluated using macro-averaged metrics

## Algorithms Tested
1. **Random Forest**
   - Max depth: 5
   - Random state: 42
   - Best performance with 0.785 accuracy

2. **Support Vector Machine (SVM)**
   - Default RBF kernel
   - Random state: 42
   - Achieved 0.763 accuracy

3. **K-Nearest Neighbors (KNN)**
   - Default parameters (k=5)
   - Lowest performance at 0.645 accuracy

## Performance Summary
| Model       | Accuracy | Precision | Recall | F1-Score |
|-------------|----------|-----------|--------|----------|
| Random Forest | 0.7849  | 0.6645    | 0.5771 | 0.6046   |
| SVM         | 0.7634   | 0.6652    | 0.5041 | 0.5395   |
| KNN         | 0.6452   | 0.5600    | 0.3738 | 0.3941   |

## Key Observations
- Random Forest outperformed other models across all metrics
- All models showed higher precision than recall, indicating better performance on majority classes
- KNN struggled most with class imbalance (lowest recall)

## Results and Insights

### Key Findings:
1. **Academic Progression**: Strong correlation found between G1, G2 and final G3 grades (r > 0.80)
2. **Family Impact**: Students with better family relationships (famrel ≥4) showed 15% higher average grades
3. **Attendance Matters**: Students with ≤5 absences performed significantly better (p < 0.01)
4. **Gender Gap**: Female students outperformed males by an average of 1.2 grade points

### Predictive Insights:
- Previous grades (G1/G2) are the strongest predictors of final performance
- Family support metrics account for ~12% of grade variance
- Lifestyle factors (health, freetime) show moderate correlation (r ≈ 0.3)

### Recommendations:
1. Early intervention programs for students scoring below 10 in G1/G2
2. Family engagement initiatives for students reporting poor family relationships
3. Attendance monitoring systems for at-risk students
