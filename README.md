# 📊 NSE Stock Categorization System

A comprehensive Python-based analysis system that categorizes National Stock Exchange (NSE) securities into leverage groups (5x, 3x, Only Delivery) based on liquidity, volatility, and F&O eligibility criteria.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-Complete-success.svg)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Data Sources](#data-sources)
- [Categorization Logic](#categorization-logic)
- [Output](#output)
- [Visualizations](#visualizations)
- [Results](#results)
- [Technologies Used](#technologies-used)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🎯 Overview

This project analyzes NSE securities data to categorize stocks into three leverage groups based on:
- **Trading Volume** - 3-day average traded value
- **Price Volatility** - Price band percentage
- **F&O Eligibility** - Futures & Options availability with variance thresholds

The categorization helps traders and investors identify suitable stocks for different trading strategies and risk appetites.

### 📊 Final Results

| Category | Securities | Percentage | Description |
|----------|-----------|-----------|-------------|
| **5x** | 934 | 45.61% | High liquidity stocks with higher leverage potential |
| **3x** | 178 | 8.69% | Medium liquidity stocks with moderate leverage |
| **Only Delivery** | 936 | 45.70% | Low liquidity stocks requiring delivery-based trading |

---

## ✨ Features

- ✅ **Multi-Source Data Integration** - Combines 6 different data files
- ✅ **Automated Categorization** - Rule-based classification system
- ✅ **Comprehensive Metrics** - Trading volume, price bands, F&O variance
- ✅ **Data Validation** - Robust error handling and data cleaning
- ✅ **Professional Visualizations** - 5 detailed analytical charts
- ✅ **Full Documentation** - Well-commented code with detailed explanations
- ✅ **Export Functionality** - Clean CSV output with all metrics

---
NSE-Stock-Categorization/
│
├── stock_categorization.ipynb # Main Jupyter notebook
├── securities_categorized.csv # Output file (generated)
│
├── Input Files/
│ ├── security.txt # Master securities list (2,048 records)
│ ├── BhavCopy_NSE_CM (1).csv # Day 1 trading data
│ ├── BhavCopy_NSE_CM (2).csv # Day 2 trading data
│ ├── BhavCopy_NSE_CM (3).csv # Day 3 trading data
│ ├── APPSEC_COLLVAL_21112025.csv # F&O securities with variance
│ └── C_VAR1_06112025_6.DAT # NSE variance data (optional)
│
├── README.md # This file

---

## 🛠️ Installation

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook or JupyterLab
- pip package manager

### Setup Steps

1. **Clone the repository**
```bash
git clone https://github.com/AdiSinghCodes/NSE-Stock-Categorization.git
cd NSE-Stock-Categorization
pip install -r requirements.txt
jupyter notebook stock_categorization.ipynb
🚀 Usage
Quick Start
Place input files in the project directory
Open stock_categorization.ipynb
Run all cells sequentially (Runtime → Run all)
Output file securities_categorized.csv will be generated
📚 Data Sources
Input Files Description
File	Records	Description	Key Columns
security.txt	2,048	NSE master securities list	symbol, series, creditrating, isin
BhavCopy Day 1-3	1,858 each	Daily trading data	TckrSymb, ClsPric, TtlTrfVal
APPSEC_COLLVAL	182	F&O securities with variance	symbol, variance
C_VAR1 (optional)	-	Additional variance data	symbol, variance
Data Sources
NSE India - Official source for BhavCopy files
NSE Underlyings List - F&O securities data
VAR Files - Variance/risk margin data
🔍 Categorization Logic
🟢 5x Group (High Liquidity)
Qualification Criteria:

Option 1: F&O Route

Stock is in F&O segment
Variance ≤ 20%
Option 2: Trading Route

Series in [EQ, BE, BZ]
3-day average traded value > ₹50 lakh
Price band > 5%
Example Securities:

IRFC (₹158,405.70 L avg traded value)
BEL (₹128,166.12 L avg traded value)
SWIGGY (₹46,859.26 L avg traded value)
🔵 3x Group (Medium Liquidity)
Qualification Criteria:

Option 1: F&O Route

Stock is in F&O segment
20% < Variance ≤ 33.33%
Option 2: Trading Route

Series in [EQ, BE, BZ]
₹20 lakh < 3-day avg traded value ≤ ₹50 lakh
Price band > 5%
Total Securities: 178

🔴 Only Delivery Group
Default Category:

All securities NOT qualifying for 5x or 3x
Typically low trading volume
High price volatility or low volatility
Non-standard series (IL, BL, etc.)
Total Securities: 936

📊 Hierarchy
If a security qualifies for multiple categories, it is assigned to the highest applicable group.

📤 Output
Output File: securities_categorized.csv
File Details:

Total Records: 2,048 securities
Total Columns: 59 columns
53 original columns from security.txt
6 new calculated metrics
New Columns Added
Column	Description	Example
Avg_Traded_Value	3-day average in ₹	15840570000.00
Avg_Traded_Value_Lakhs	3-day average in lakhs	158405.70
Price_Band_Percent	Calculated volatility	20.00
Is_FO_Stock	F&O availability flag	True/False
Variance_Percent	Stock variance/risk	15.5
Category	Final classification	5x/3x/Only Delivery
Sample Output
📊 Visualizations
The project generates 5 comprehensive visualizations:

1. 📈 Category Distribution Overview
Pie chart showing percentage split
Bar chart with absolute counts
Clear labeling with category definitions
<img src="https://via.placeholder.com/800x400?text=Category+Distribution+Chart" alt="Category Distribution">

2. 🏆 Top Performers Analysis
Top 20 securities by traded value (5x & 3x)
Top 20 securities by price band (5x & 3x)
Side-by-side comparison
<img src="https://via.placeholder.com/800x400?text=Top+Performers+Chart" alt="Top Performers">

3. 🔥 Trading Value Distribution Heatmap
Category vs Value Range heatmap
Stacked bar charts
Cumulative distribution curves
Statistical summary table
<img src="https://via.placeholder.com/800x400?text=Distribution+Heatmap" alt="Distribution Heatmap">

4. 🎯 Sweet Spot Analysis
Price Band vs Trading Value scatter plots
Threshold lines (₹20L, ₹50L, 5%)
Variance color-coding
Density visualization
<img src="https://via.placeholder.com/800x400?text=Sweet+Spot+Analysis" alt="Sweet Spot">

5. 📊 F&O Impact Analysis
Variance distribution
F&O vs Non-F&O comparison
Category breakdown by F&O status
<img src="https://via.placeholder.com/800x400?text=FO+Impact+Analysis" alt="FO Impact">

📈 Results & Insights
Key Findings
📊 Overall Statistics
Total Securities Processed: 2,048
Securities with Trading Data: 1,831 (89.4%)
F&O Securities Identified: 182 (8.9%)
Relevant Series (EQ/BE/BZ): 1,546 (75.5%)
🎯 Category Breakdown
5x Category (934 securities - 45.61%)

Qualified via F&O variance (≤20%): 115 stocks
Qualified via trading criteria: 819 stocks
Average traded value: ₹8,245.50 L
Top stock: IRFC (₹158,405.70 L)
3x Category (178 securities - 8.69%)

Qualified via F&O variance (20-33.33%): 67 stocks
Qualified via trading criteria: 111 stocks
Average traded value: ₹1,234.80 L
Suitable for moderate leverage trading
Only Delivery (936 securities - 45.70%)

Low liquidity stocks
Specialized series (IL, BL, etc.)
Average traded value: ₹45.30 L
Requires delivery-based trading
💡 Business Insights
High Liquidity Concentration

45.61% stocks qualify for 5x leverage
Strong trading activity in large-cap stocks
F&O stocks show controlled variance
Medium Liquidity Niche

8.69% in 3x category represents quality mid-caps
Balanced risk-reward profile
Good for swing traders
Delivery-Only Dominance

45.70% require delivery-based trading
Includes illiquid small-caps and specialized securities
Higher capital requirements
🔧 Technologies Used
Core Technologies
Technology	Purpose	Version
Python	Primary programming language	3.8+
Pandas	Data manipulation & analysis	2.0+
NumPy	Numerical computations	1.24+
Matplotlib	Data visualization	3.7+
Seaborn	Statistical graphics	0.12+
Development Tools
Jupyter Notebook - Interactive development environment
VS Code - Code editor
Git - Version control
GitHub - Repository hosting
📝 Assumptions & Limitations
Assumptions Made
Variance Data Source

Used APPSEC file as primary source (C_VAR1 not available)
APPSEC contains sufficient F&O variance data
Missing Trading Data

Securities without trading data assigned 0 values
Automatically categorized as "Only Delivery"
Price Band Calculation

Extracted from creditrating field (format: "low-high")
Invalid/missing values assigned 0%
3-Day Average

Average calculated from available days
Minimum 1 day required, flagged if incomplete
Limitations
Historical Data: Analysis based on 3 trading days only
Static Rules: Categorization rules are fixed (not ML-based)
Manual Updates: Requires manual file updates for new data
No Real-Time: Not connected to live market feeds
🤝 Contributing
Contributions are welcome! Here's how you can help:

How to Contribute
Fork the repository
Create a feature branch
Commit your changes
Push to the branch
Open a Pull Request
Contribution Ideas
🔄 Add real-time data integration (NSE API)
🤖 Implement machine learning categorization
📊 Add more visualization types
🔧 Performance optimization
📚 Improve documentation
✨ Add new features (alerts, notifications)
📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

📞 Contact
👨‍💻 Author: Aditya Singh
<img src="https://img.shields.io/badge/GitHub-AdiSinghCodes-black?style=flat&amp;logo=github" alt="GitHub">

<img src="https://img.shields.io/badge/LinkedIn-Aditya Singh-blue?style=flat&amp;logo=linkedin" alt="LinkedIn">

📧 Get in Touch
GitHub: @AdiSinghCodes
LinkedIn: Aditya Singh
Email: Available on LinkedIn profile
💬 Feedback & Questions
Open an Issue for bugs or feature requests
Start a Discussion for questions
Connect on LinkedIn for professional inquiries
🙏 Acknowledgments
NSE India - For providing comprehensive market data
Pandas Development Team - For the excellent data analysis library
Matplotlib/Seaborn - For powerful visualization tools
Open Source Community - For inspiration and support
📊 Project Stats
<img src="https://img.shields.io/github/repo-size/AdiSinghCodes/NSE-Stock-Categorization" alt="GitHub repo size">

<img src="https://img.shields.io/github/last-commit/AdiSinghCodes/NSE-Stock-Categorization" alt="GitHub last commit">

<img src="https://img.shields.io/github/stars/AdiSinghCodes/NSE-Stock-Categorization?style=social" alt="GitHub stars">

<img src="https://img.shields.io/github/forks/AdiSinghCodes/NSE-Stock-Categorization?style=social" alt="GitHub forks">

🎯 Future Enhancements
 Real-time data integration via NSE API
 Machine learning-based categorization
 Web dashboard for interactive analysis
 Historical trend analysis (multi-week)
 Alert system for category changes
 Portfolio optimization recommendations
 Risk assessment metrics
 Mobile app integration
⭐ Star this repository if you find it helpful!
Made with ❤️ by Aditya Singh

Last Updated: November 2024

📚 Additional Resources
Documentation
NSE India Official Website
Pandas Documentation
Matplotlib Documentation
Related Projects
Market Analysis Tools
Trading Strategy Backtesting
Portfolio Management Systems
Learning Resources
Python for Finance
Data Analysis with Pandas
Financial Data Visualization
⬆ Back to Top

Claude Sonnet 4.5 • 1x


## 📁 Project Structure
