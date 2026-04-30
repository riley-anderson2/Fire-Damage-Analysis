# Fire Damage Analysis: Modeling the Impact of Fire Station Proximity on Residential Fire Damage

## Summary

This project presents a comprehensive statistical analysis examining the relationship between fire station proximity and residential fire damage using simple linear regression and model comparison techniques. The analysis of 15 residential fires in a major suburban region reveals a **statistically significant positive linear relationship**: for every mile increase in distance from the nearest fire station, expected fire damage increases by **$4,919** (R² = 0.923).

---

## Table of Contents
- [Project Overview](#project-overview)
- [Research Question & Motivation](#research-question--motivation)
- [Dataset Description](#dataset-description)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Technical Implementation](#technical-implementation)
- [Files & Structure](#files--structure)
- [How to Reproduce](#how-to-reproduce)
- [Conclusions & Recommendations](#conclusions--recommendations)

---

## Project Overview

### Purpose
This analysis addresses a practical problem for urban planning and public safety: **Does fire station location significantly influence residential fire damage?** The findings inform decisions about optimal fire station placement to minimize property damage in suburban residential areas.

### Context
A fire insurance company commissioned this analysis to understand the relationship between:
- **Independent Variable**: Distance from nearest fire station (miles)
- **Dependent Variable**: Monetary damage from fire (thousands of dollars)

### Key Question
*Does increased distance from a fire station lead to proportionally higher fire damage in residential areas, and can we build a reliable predictive model?*

---

## Research Question & Motivation

### Context
Fire insurance companies must accurately model risk to set appropriate premiums and identify high-risk zones. Understanding the impact of fire station proximity enables:
- **Risk Assessment**: Accurate pricing based on fire station distance
- **Urban Planning**: Data-driven recommendations for fire station placement
- **Resource Allocation**: Identification of underserved areas requiring additional coverage
- **Damage Prevention**: Protection of residential properties through infrastructure optimization

### Hypothesis
We hypothesize a **positive linear relationship** between distance from fire station and fire damage, based on the principle that firefighter response time directly impacts fire containment capability and ultimate damage extent.

---

## Dataset Description

### Sample
- **Sample Size**: 15 recent residential fires in a large suburb
- **Geographic Scope**: Single major suburban area

### Variables

| Variable | Type | Unit | Range | Description |
|----------|------|------|-------|-------------|
| **DISTANCE** | Quantitative, Continuous | Miles | 0.7 – 6.1 | Absolute straight-line distance from nearest fire station |
| **DAMAGE** | Quantitative, Continuous | Thousands USD | $2.2k – $26.1k | Monetary loss due to fire damage |

### Data Collection Notes
- Distance measured as absolute straight-line distance (not road distance)
- Damage represents total monetary loss
- Fires were sampled across time to reduce temporal bias
- Limited documentation of collection methodology suggests random sampling across the suburban area

---

## Methodology

### Statistical Approach

#### 1. **Simple Linear Regression (SLR)**
Proposed model:
$$y = \beta_0 + \beta_1 x + \epsilon$$

Where:
- $y$ = damage (thousands of dollars)
- $x$ = distance (miles)
- $\beta_0$ = intercept (baseline damage)
- $\beta_1$ = slope (damage increase per mile)
- $\epsilon$ = error term

#### 2. **Model Assumptions & Verification**
All SLR models require four critical assumptions about the error term:

| Assumption | Test Used | Result |
|-----------|-----------|--------|
| **Linearity** | Scatter plot + Lowess smoother | ✓ Supported (trend remains linear across range) |
| **Normality** | Shapiro-Wilk test (H₀: ε ~ N) | ✓ Supported (W = 0.977, p > 0.05) |
| **Homoscedasticity** | Residuals vs. Fitted plot | ✓ Mostly supported (constant variance, slight U-shape) |
| **Independence** | Contextual reasoning | ✓ Assumed (fires sampled across time/location) |

#### 3. **Model Comparison: Linear vs. Quadratic**
To address the slight U-shape in residuals, we compared:
- **Linear Model**: $\hat{y} = 4.919x + 10.278$
- **Quadratic Model**: $\hat{y} = 13.350 + 2.64x + 0.338x^2$

**Model Selection Criteria**:
- Quadratic model showed only marginal R² improvement (0.923 → 0.926)
- Confidence interval for quadratic term includes zero: CI = (-0.174, 0.849)
- Hypothesis test: Failed to reject H₀: β₂ = 0 (p > 0.05)
- **Conclusion**: Linear model preferred for parsimony and statistical significance

#### 4. **Influence & Outlier Detection**
- Used Cook's Distance to identify influential observations
- Threshold: D_i > 4/n = 0.267 for n=15
- Observation 13 exceeded threshold but removal decreased R²
- Retained full dataset for final model

### Model Diagnostics
All diagnostic plots generated to validate assumptions:
- ✓ Linearity confirmed through exploratory plots
- ✓ Residual scatter around zero with no systematic pattern
- ✓ Normal Q-Q plot confirms approximate normality
- ✓ Scale-location plot confirms homoscedasticity

---

## Key Findings

### Primary Result: Linear Model Estimates

**Fitted Model**:
$$\hat{y} = 4.919x + 10.278$$

**Interpretation**:
- **Intercept (β₀ = 10.278)**: Expected baseline damage of ~$10,278 (note: extrapolation beyond observed range of 0.7–6.1 miles)
- **Slope (β₁ = 4.919)**: **Each additional mile from fire station increases expected damage by $4,919**
- **Practical Impact**: A fire 2 miles further away costs an additional ~$9,838 in damage on average

### Model Performance Metrics

| Metric | Value | Interpretation |
|--------|-------|-----------------|
| **R-squared (R²)** | 0.923 | Model explains 92.3% of variance in damage |
| **Adjusted R²** | 0.918 | Accounts for sample size; minimal penalty applied |
| **Correlation** | Strong positive | Distance and damage highly correlated |

### Predictive Examples
Using the fitted model for distance-based damage prediction:
- **2 miles**: $19.695k expected damage
- **4 miles**: $29.553k expected damage  
- **5.5 miles**: $37.717k expected damage

### Statistical Significance
- Relationship is **statistically significant** at α = 0.05
- Confidence intervals for slope estimate: approx (3.4, 6.4) [95% CI]
- Results support the hypothesis of a meaningful linear relationship

---

## Technical Implementation

### Tools & Languages
- **Language**: R (v4.x)
- **Document Format**: R Markdown with HTML/PDF/Word output
- **Packages Used**:
  - `DT` - Interactive data tables
  - `s20x` - Statistical graphics (trendscatter, normcheck, cooks20x)
  - Base R for core statistical analysis

### Analyses Performed

1. **Exploratory Data Analysis**
   - Descriptive statistics
   - Scatter plots with visual trend analysis
   - Interactive data tables

2. **Linear Model Fitting**
   - Least-squares parameter estimation
   - Coefficient interpretation
   - Confidence interval calculation

3. **Variance Decomposition**
   - RSS (Residual Sum of Squares)
   - MSS (Model Sum of Squares)
   - TSS (Total Sum of Squares)
   - R² calculation and interpretation

4. **Assumption Verification**
   - Normality testing (Shapiro-Wilk)
   - Homoscedasticity assessment
   - Linearity verification
   - Independence evaluation

5. **Model Comparison**
   - Quadratic model fitting
   - Coefficient significance testing
   - R² comparison
   - Parsimony vs. accuracy trade-off

6. **Influence Diagnostics**
   - Cook's Distance calculation
   - Outlier assessment
   - Robustness checking

---

## Files & Structure

```
Fire-Damage-Analysis/
├── README.md                      # This file
├── FireDamageAnalysis.Rmd        # Source R Markdown document
├── FireDamageAnalysis.html       # Generated HTML report with visualizations
├── FireDamageAnalysis.pptx       # Presentation summary
├── FIREDAM.csv                    # Raw dataset (15 observations)
├── project.bib                    # Bibliography/references
├── biomed-central.csl             # Citation style file
└── LICENSE                        # Project license
```

### Generated Outputs
The HTML version includes:
- Interactive data table with filtering/export capabilities
- Publication-quality graphics with captions
- Mathematical notation and equations
- Responsive table of contents
- Code folding for cleaner presentation

---

## How to Reproduce

### Prerequisites
- **R** (v3.5+) with core packages
- **RMarkdown** package (`install.packages("rmarkdown")`)
- **s20x** package (`install.packages("s20x")`)
- **DT** package (`install.packages("DT")`)

### Steps to Run

1. **Clone/Navigate to repository**:
   ```r
   setwd("path/to/Fire-Damage-Analysis")
   ```

2. **Load the data**:
   ```r
   fire <- read.csv("FIREDAM.csv")
   ```

3. **Render the R Markdown document**:
   ```r
   rmarkdown::render("FireDamageAnalysis.Rmd", 
                     output_format = "html_document")
   ```

4. **View output**:
   Open `FireDamageAnalysis.html` in your browser

### Customization
The Rmd file is fully commented and structured to allow:
- Parameter changes (confidence levels, thresholds)
- Alternative model specifications
- Additional diagnostic plots
- Extended analyses

---

## Conclusions & Recommendations

### Main Conclusions

1. **Confirmed Relationship**: Strong evidence (R² = 0.923) supports a **positive linear relationship** between fire station distance and residential fire damage

2. **Practical Magnitude**: The effect is **economically significant**—each additional mile increases damage by ~$4,919, suggesting distance is a material factor in fire damage outcomes

3. **Model Appropriateness**: Linear model is more appropriate than quadratic despite slight residual pattern, justified by:
   - Insignificant quadratic coefficient
   - Minimal R² improvement
   - Principle of parsimony

4. **Assumption Compliance**: All SLR assumptions adequately satisfied, supporting model validity and inference

### Practical Applications

- **Insurance Pricing**: Distance-based risk premiums for residential fire insurance
- **Urban Planning**: Justifies investment in fire station infrastructure in distant suburban areas
- **Emergency Response**: Evidence supporting strategic placement to maximize damage mitigation
- **Risk Management**: Enables identification of high-risk (distant) zones for additional prevention measures

### Limitations & Future Improvements

**Current Limitations**:
- Small sample size (n=15) limits generalizability
- Single geographic region; unclear if results apply nationally
- Straight-line distance may not reflect actual response routes
- Limited temporal coverage (specific time period)

## Author

**Riley Anderson**  

**Project Status**: ✓ Complete | **Last Updated**: April 30, 2026
