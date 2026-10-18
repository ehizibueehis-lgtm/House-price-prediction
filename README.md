# Multiple Linear Regression - House Price Prediction

## Project Objective
To preprocess a messy housing dataset and build a Multiple Linear Regression model capable of estimating house prices based on features like size, location, and property type.

## Project Structure
* `charts/`: Contains the evaluation visualizations (Actual vs Predicted, Residual Plot, Metrics Summary).
* `house_price_regression.py`: The main script for data preprocessing, model training, and evaluation.
* `data/cleaned_housing_data.csv`: The final, clean dataset of 1,911 records.
* `requirements.txt`: Python dependencies required to run the script.

## Setup Instructions
1. Clone this repository.
2. Install the required packages using `pip install -r requirements.txt`.
3. Run the script to generate the cleaned data, train the model, and view the charts.

## Model Evaluation & Findings

**Which features were used to predict house price?**
The model utilized nine original features to predict house prices: Property Size (SqFt), Bedrooms, Bathrooms, Garage Spaces, Property Age (Years), Distance to City Center (Km), Location, Property Type, and Garden Availability. After One-Hot Encoding the categorical variables, these were expanded into 16 numerical features for the model.

**What preprocessing problems did you discover and how did you handle them?**
The dataset contained several critical data-quality issues:
*   **Mixed Data Types:** Numerical columns (Size, Bedrooms, Age) contained text strings (e.g., "3052 sqft", "three", "new"). I handled this by using regular expressions to strip alphabetical characters, mapping spelled-out words to digits, and forcing the columns to float types.
*   **Inconsistent Categories:** Columns like `Location` and `Property_Type` had varied capitalization and whitespace. I standardized these using string stripping and Title Case. The `Has_Garden` column had multiple variations (Y, yes, N, no), which I mapped to a clean binary "Yes" or "No".
*   **Missing Data & Duplicates:** I dropped 69 total duplicate rows (62 exact copies and 7 hidden duplicates exposed during text standardization). I also dropped 10 rows missing the target `House_Price` and filtered out 10 rows with impossible data (e.g., 0 square feet). I imputed the remaining missing values using the median for numerical columns and the mode for categorical ones.

**What do your MSE, RMSE, and $R^{2}$ results suggest about model performance?**
The model achieved an $R^{2}$ of 0.9184, successfully explaining 91.84% of the variance in house prices. The RMSE of approximately 8.5 million Naira indicates that predictions deviate by an average of 8,568,053 Naira from the actual price. Removing the hidden duplicates directly improved the RMSE by over 500,000 Naira per prediction. While the MSE remains massively inflated (over 73 trillion) due to squaring the errors, the tightened RMSE and strong $R^{2}$ confirm a highly accurate fit without indicating severe overfitting.

**From the actual-vs-predicted and residual plots, where does the model appear to perform well or poorly?**
The actual-vs-predicted scatter plot shows a strong linear grouping along the perfect prediction line, indicating reliable performance across most of the dataset. The residual plot shows a relatively even, random scatter of errors above and below the zero line (homoscedasticity). However, the model appears to struggle slightly more with extreme outliers—particularly underpredicting some of the most expensive properties.

**What limitations does this model or dataset have?**
Multiple Linear Regression assumes a strictly straight-line relationship between the features and the price, which may not capture complex real-world pricing dynamics. Additionally, the dataset is limited to basic structural features and distance metrics; it lacks nuanced variables that heavily influence real estate, such as neighborhood safety, architectural condition, or proximity to specific amenities (schools, markets).

**What could you try in the future to improve the model?**
To improve accuracy, we could engineer new features, such as calculating the "Price per Square Foot." We could also experiment with non-linear Machine Learning models, such as Random Forest or Gradient Boosting (XGBoost), which are better equipped to handle complex feature interactions and outliers than standard Linear Regression.