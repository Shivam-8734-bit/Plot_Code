import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
file_path = "Marks_secC.xlsx"  # Ensure this file is in the same directory or provide full path
df = pd.read_excel(file_path)

# Extract relevant columns
df_clean = df.iloc[:, [0, 1, 6]].copy()
df_clean.columns = ['Roll Number', 'Name', 'Marks']

# Drop rows with missing marks
df_clean = df_clean.dropna(subset=['Marks'])

# Calculate percentage
df_clean['Percentage'] = (df_clean['Marks'] / 15) * 100

# Categorize students
above_75 = df_clean[df_clean['Percentage'] > 75]
between_60_75 = df_clean[(df_clean['Percentage'] >= 60) & (df_clean['Percentage'] <= 75)]
below_60 = df_clean[df_clean['Percentage'] < 60]

# Print categorized data
print("\n--- Students with >75% ---")
print(above_75[['Roll Number', 'Name', 'Percentage']])

print("\n--- Students with 60% - 75% ---")
print(between_60_75[['Roll Number', 'Name', 'Percentage']])

print("\n--- Students with <60% ---")
print(below_60[['Roll Number', 'Name', 'Percentage']])

# Plot Histogram
plt.figure(figsize=(10, 5))
plt.hist(df_clean['Percentage'], bins=range(0, 105, 5), edgecolor='black', color='blue')
plt.xlabel('Percentage')
plt.ylabel('Number of Students')
plt.title('Histogram Plot')
plt.grid(True)
plt.tight_layout()
plt.show()

# Plot Scatter
plt.figure(figsize=(12, 5))
plt.scatter(range(len(df_clean)), df_clean['Percentage'], color='blue')
plt.xlabel('Students')
plt.ylabel('Percentage')
plt.title('Scatter Plot')
plt.grid(True)
plt.tight_layout()
plt.show()
