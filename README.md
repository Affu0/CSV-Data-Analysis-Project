# CSV-Data-Analysis-Project
import csv
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Create CSV data
data = [
    ["Name", "Age", "City"],
    ["Alice", 25, "New York"],
    ["Bob", 30, "Los Angeles"],
    ["Charlie", 27, "Chicago"],
    ["John", 33, "Mexico"],
    ["Maria", 31, "South Africa"],
    ["Aafiya", 22, "India"],
    ["Nick", 29, "Chicago"],
    ["Abeba", 25, "Paris"],
    ["Nikitha", 29, "Chennai"]
]

with open("data.csv", mode="w", newline="") as file:
    writer = csv.writer(file)
    writer.writerows(data)

print("CSV file created successfully.")

# Load dataset
df = pd.read_csv("data.csv")

# Display first few rows
print("\nFirst 5 rows:")
print(df.head())

# Basic statistics (only for numeric columns)
print("\nBasic Statistics:")
print(df.describe())

# Check for missing values
print("\nMissing values:")
print(df.isnull().sum())

# Convert "Age" column to numeric (in case it's read as a string)
df["Age"] = pd.to_numeric(df["Age"], errors="coerce")

# Data visualization

# 1. Histogram for Age distribution
plt.figure(figsize=(8, 5))
sns.histplot(df["Age"], bins=5, kde=True, color="black")
plt.title("Age Distribution")
plt.xlabel("Age")
plt.ylabel("Count")
plt.show()

# 2. Count plot for City distribution
plt.figure(figsize=(8, 5))
sns.countplot(y=df["City"], palette="viridis")
plt.title("City Distribution")
plt.xlabel("Count")
plt.ylabel("City")
plt.show()

# 3. Correlation heatmap (only for numeric columns)
plt.figure(figsize=(5, 2))
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap="coolwarm", fmt=".2f")
plt.title("Correlation Heatmap")
plt.show()
