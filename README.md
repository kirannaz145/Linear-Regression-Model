
# Project Title

A brief description of what this project does and who it's for


## 🚀 About Me
I'm a full stack developer...

import pandas as pd
import numpy as np
import statsmodels.api as sm
from sklearn.metrics import mean_squared_error

# Load the Excel file
file_path = "/content/RMSE.xlsx"
df = pd.read_excel(file_path)

# Extract the first extended energy as the independent variable (first column)
X = df.iloc[:, 0]  # First extended energy
X = sm.add_constant(X)  # Add intercept

# Extract BP as the dependent variable
y = df["BP"]

# Fit the model
model = sm.OLS(y, X).fit()

# Extract statistics
r_squared = model.rsquared
rmse = np.sqrt(mean_squared_error(y, model.fittedvalues))
standard_error = model.bse[1]  # Standard error of coefficient
f_statistic = model.fvalue
p_value = model.pvalues[1]  # p-value of coefficient

# Print regression equation
coef = model.params
equation = f"BP = {coef[0]:.3f} + {coef[1]:.3f} × First Extended Energy"

print("Equation for BP:")
print(equation)
print(f"R² = {r_squared:.3f}, RMSE = {rmse:.3f}, ζₑ = {standard_error:.3f}, F = {f_statistic:.3f}, ∇ = {p_value:.3f}")
