# Task-2
Unemployment Analysis with Python
import os
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

def analyze_unemployment(file_path):
    if not os.path.exists(file_path):
        print(f"Error: File '{file_path}' not found.")
        return
    
    # Load the dataset
    df = pd.read_csv(file_path)
    
    # Clean column names (remove leading/trailing spaces)
    df.columns = df.columns.str.strip()
    
    # Convert date column to datetime if applicable
    if 'Date' in df.columns:
        df['Date'] = pd.to_datetime(df['Date'], errors='coerce')
    
    # Display basic info and first few rows
    print("Dataset Info:\n", df.info())
    print("\nFirst Five Rows:\n", df.head())
    
    # Checking for missing values
    print("\nMissing Values:\n", df.isnull().sum())
    
    # Summary statistics
    print("\nSummary Statistics:\n", df.describe())
    
    # Unemployment rate trends visualization
    plt.figure(figsize=(12, 6))
    sns.lineplot(x='Date', y='Estimated Unemployment Rate (%)', data=df)
    plt.xticks(rotation=45)
    plt.xlabel('Date')
    plt.ylabel('Unemployment Rate (%)')
    plt.title('Unemployment Rate Over Time')
    plt.show()
    
    # Unemployment rate distribution
    plt.figure(figsize=(8, 5))
    sns.histplot(df['Estimated Unemployment Rate (%)'].dropna(), bins=20, kde=True)
    plt.title('Distribution of Unemployment Rate')
    plt.xlabel('Unemployment Rate (%)')
    plt.ylabel('Frequency')
    plt.show()
    
    # Unemployment by state (if applicable)
    if 'Region' in df.columns:
        plt.figure(figsize=(15, 6))
        sns.barplot(x='Region', y='Estimated Unemployment Rate (%)', data=df)
        plt.xticks(rotation=90)
        plt.title('Unemployment Rate by Region')
        plt.xlabel('Region')
        plt.ylabel('Unemployment Rate (%)')
        plt.show()

# Run the function with the uploaded dataset
file_path = "/mnt/data/Unemployment in India.csv"
analyze_unemployment(file_path)[Unemployment in India.csv](https://github.com/user-attachments/files/18795938/Unemployment.in.India.csv)
