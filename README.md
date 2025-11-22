# 📊 NSE Stock Categorization System

A comprehensive Python-based analysis system that categorizes National Stock Exchange (NSE) securities into leverage groups (5x, 3x, Only Delivery) based on liquidity, volatility, and F&O eligibility criteria.

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-Active-success.svg)

---

## 🎯 Overview

This project analyzes NSE securities data to automatically categorize stocks into three leverage groups based on:
- **Trading Volume** - 3-day average traded value analysis
- **Price Volatility** - Price band percentage calculations
- **F&O Eligibility** - Futures & Options availability with variance thresholds

The categorization helps traders and investors identify suitable stocks for different trading strategies and risk profiles, enabling informed decision-making for intraday, swing, and delivery-based trading.

### 📈 Quick Results

| Category | Count | Percentage | Description |
|----------|-------|-----------|-------------|
| **5x Leverage** | 934 | 45.61% | High liquidity stocks suitable for higher leverage trading |
| **3x Leverage** | 178 | 8.69% | Medium liquidity stocks with moderate leverage potential |
| **Only Delivery** | 936 | 45.70% | Low liquidity stocks requiring delivery-based trading |

**Total Securities Analyzed:** 2,048

---

## ✨ Key Features

- ✅ **Multi-Source Data Integration** - Combines 6 different NSE data files seamlessly
- ✅ **Intelligent Categorization** - Dual-path classification (F&O route + Trading volume route)
- ✅ **Comprehensive Metrics** - Analyzes trading volume, price bands, and F&O variance
- ✅ **Data Validation** - Robust error handling and data quality checks
- ✅ **Rich Visualizations** - 5 professional analytical charts with insights
- ✅ **Production-Ready Output** - Clean CSV export with 59 columns of metrics
- ✅ **Well-Documented Code** - Detailed comments and explanations throughout

---

## 📁 Project Structure

```
NSE-Stock-Categorization/
│
├── stock_categorization.ipynb      # Main Jupyter notebook with analysis
├── securities_categorized.csv      # Generated output file
├── requirements.txt                # Python dependencies
├── README.md                       # This documentation
│
└── Input Files/                    # Place your data files here
    ├── security.txt                # Master securities list (2,048 records)
    ├── BhavCopy_NSE_CM (1).csv    # Trading data - Day 1
    ├── BhavCopy_NSE_CM (2).csv    # Trading data - Day 2
    ├── BhavCopy_NSE_CM (3).csv    # Trading data - Day 3
    ├── APPSEC_COLLVAL_21112025.csv # F&O securities with variance data
    └── C_VAR1_06112025_6.DAT      # NSE variance data (optional)
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook or JupyterLab
- pip package manager

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/AdiSinghCodes/NSE-Stock-Categorization.git
   cd NSE-Stock-Categorization
   ```

2. **Install required packages**
   ```bash
   pip install -r requirements.txt
   ```

3. **Prepare your data files**
   - Download the required files from NSE India website
   - Place them in the project root or `Input Files/` directory
   - Ensure file names match those specified in the notebook

4. **Run the analysis**
   ```bash
   jupyter notebook stock_categorization.ipynb
   ```
   Run all cells in sequence to generate the categorized output.

### Required Python Packages

```
pandas>=2.0.0
numpy>=1.24.0
matplotlib>=3.7.0
seaborn>=0.12.0
```

---

## 📊 Input Data Sources

### File Descriptions

| File | Records | Purpose | Key Columns |
|------|---------|---------|-------------|
| `security.txt` | 2,048 | NSE master securities list | symbol, series, creditrating, isin |
| `BhavCopy_NSE_CM (1-3).csv` | ~1,858 each | Daily trading data (3 days) | TckrSymb, ClsPric, TtlTrfVal |
| `APPSEC_COLLVAL_*.csv` | 182 | F&O securities with variance | symbol, variance |
| `C_VAR1_*.DAT` | Variable | Additional variance data (optional) | symbol, variance |

### Data Sources

- **NSE India Official Portal** - [BhavCopy Downloads](https://www.nseindia.com/market-data/all-upcoming-issues-ipo)
- **F&O Underlying List** - [NSE Derivatives](https://www.nseindia.com/derivatives)
- **Variance Files** - Available through NSE member portal

---

## 🔍 Categorization Logic

### 🟢 5x Leverage Group (High Liquidity)

**Qualification Criteria:**

**Path 1: F&O Route**
- Stock is listed in F&O segment
- Variance ≤ 20%

**Path 2: Trading Volume Route**
- Series in [EQ, BE, BZ]
- 3-day average traded value > ₹50 lakh
- Price band > 5%

**Example Securities:**
- IRFC (₹1,58,405.70 L avg traded value)
- BEL (₹1,28,166.12 L avg traded value)
- SWIGGY (₹46,859.26 L avg traded value)

---

### 🔵 3x Leverage Group (Medium Liquidity)

**Qualification Criteria:**

**Path 1: F&O Route**
- Stock is listed in F&O segment
- 20% < Variance ≤ 33.33%

**Path 2: Trading Volume Route**
- Series in [EQ, BE, BZ]
- ₹20 lakh < 3-day avg traded value ≤ ₹50 lakh
- Price band > 5%

**Total Securities:** 178

---

### 🔴 Only Delivery Group

**Characteristics:**
- All securities NOT qualifying for 5x or 3x categories
- Typically low trading volume (< ₹20 lakh daily)
- May have high price volatility or restricted series
- Non-standard series codes (IL, BL, etc.)

**Total Securities:** 936

---

### Classification Hierarchy

If a security qualifies for multiple categories, it is assigned to the **highest applicable group** (5x > 3x > Only Delivery).

---

## 📤 Output Details

### Generated File: `securities_categorized.csv`

**File Specifications:**
- **Total Records:** 2,048 securities
- **Total Columns:** 59
  - 53 original columns from `security.txt`
  - 6 newly calculated metrics

### New Calculated Columns

| Column | Description | Example Value |
|--------|-------------|---------------|
| `Avg_Traded_Value` | 3-day average in ₹ | 15840570000.00 |
| `Avg_Traded_Value_Lakhs` | 3-day average in lakhs | 158405.70 |
| `Price_Band_Percent` | Calculated volatility % | 20.00 |
| `Is_FO_Stock` | F&O availability (True/False) | True |
| `Variance_Percent` | Stock variance/risk margin | 15.5 |
| `Category` | Final classification | 5x / 3x / Only Delivery |

### Sample Output Rows

```csv
symbol,series,Avg_Traded_Value_Lakhs,Price_Band_Percent,Is_FO_Stock,Variance_Percent,Category
IRFC,EQ,158405.70,20.0,False,0.0,5x
BEL,EQ,128166.12,20.0,True,12.5,5x
RELIANCE,EQ,85432.50,10.0,True,8.0,5x
MIDCAPSECURE,EQ,35.40,5.0,False,0.0,Only Delivery
```

---

## 📊 Visualizations

The project generates **5 comprehensive visualizations** to help understand categorization patterns:

### 1. 📈 Category Distribution Overview
- Pie chart showing percentage distribution
- Bar chart with absolute counts
- Clear labeling with category descriptions

### 2. 🏆 Top Performers Analysis
- Top 20 securities by traded value (5x & 3x groups)
- Top 20 securities by price band volatility
- Side-by-side comparative analysis

### 3. 🔥 Trading Value Distribution Heatmap
- Category vs Value Range correlation
- Stacked distribution bars
- Cumulative percentage curves
- Statistical summary tables

### 4. 🎯 Sweet Spot Analysis
- Price Band vs Trading Value scatter plots
- Visual threshold markers (₹20L, ₹50L, 5% band)
- F&O variance color-coding
- Trading density visualization

### 5. 📊 F&O Impact Analysis
- Variance distribution across categories
- F&O vs Non-F&O comparison metrics
- Category breakdown by F&O status
- Risk-return relationship mapping

---

## 📈 Key Insights & Findings

### Overall Statistics

- **Total Securities Processed:** 2,048
- **Securities with Trading Data:** 1,831 (89.4%)
- **F&O Securities Identified:** 182 (8.9%)
- **Relevant Series (EQ/BE/BZ):** 1,546 (75.5%)

### Category-wise Analysis

#### 🟢 5x Category (934 securities - 45.61%)
- **Via F&O variance (≤20%):** 115 stocks
- **Via trading criteria:** 819 stocks
- **Average traded value:** ₹8,245.50 lakhs
- **Top performer:** IRFC (₹1,58,405.70 L)
- **Characteristics:** Large-cap stocks, high liquidity, controlled risk

#### 🔵 3x Category (178 securities - 8.69%)
- **Via F&O variance (20-33.33%):** 67 stocks
- **Via trading criteria:** 111 stocks
- **Average traded value:** ₹1,234.80 lakhs
- **Characteristics:** Quality mid-caps, balanced risk-reward, suitable for swing trading

#### 🔴 Only Delivery (936 securities - 45.70%)
- **Average traded value:** ₹45.30 lakhs
- **Characteristics:** Small-caps, illiquid stocks, specialized series
- **Trading style:** Long-term delivery-based only

### Business Implications

1. **High Liquidity Concentration:** Nearly half of all NSE stocks qualify for 5x leverage, indicating strong trading activity in large-cap segment

2. **Quality Mid-cap Niche:** The 3x category represents a selective group of medium-liquidity stocks with growth potential

3. **Delivery-Only Requirement:** 45.7% of stocks require delivery-based trading due to liquidity constraints, emphasizing the importance of capital allocation

4. **F&O Effect:** Stocks in F&O segment show controlled variance, making them suitable for leveraged trading

---

## 🛠️ Technologies Used

| Technology | Purpose | Version |
|------------|---------|---------|
| **Python** | Core programming language | 3.8+ |
| **Pandas** | Data manipulation & analysis | 2.0+ |
| **NumPy** | Numerical computations | 1.24+ |
| **Matplotlib** | Data visualization | 3.7+ |
| **Seaborn** | Statistical graphics | 0.12+ |
| **Jupyter** | Interactive development | Latest |

---

## 🔧 Usage Examples

### Basic Usage

```python
# Run the complete analysis
import pandas as pd

# Load the categorized output
df = pd.read_csv('securities_categorized.csv')

# Filter 5x leverage stocks
high_leverage = df[df['Category'] == '5x']

# Get top 10 by trading volume
top_volume = high_leverage.nlargest(10, 'Avg_Traded_Value_Lakhs')
print(top_volume[['symbol', 'Avg_Traded_Value_Lakhs', 'Category']])
```

### Custom Filtering

```python
# Find F&O stocks in 5x category with low variance
safe_fo_stocks = df[
    (df['Category'] == '5x') & 
    (df['Is_FO_Stock'] == True) & 
    (df['Variance_Percent'] < 15)
]

# Get medium volatility 3x stocks
moderate_volatility = df[
    (df['Category'] == '3x') & 
    (df['Price_Band_Percent'] >= 5) & 
    (df['Price_Band_Percent'] <= 10)
]
```

---

## 📝 Important Assumptions & Limitations

### Assumptions

1. **Variance Data Source:** APPSEC_COLLVAL file used as primary source (C_VAR1 file is optional)
2. **Missing Trading Data:** Securities without trading data are assigned 0 values and categorized as "Only Delivery"
3. **Price Band Extraction:** Calculated from `creditrating` field (format: "low-high")
4. **3-Day Average:** Calculated from available days; minimum 1 day required
5. **Series Codes:** EQ, BE, BZ considered standard trading series

### Limitations

- **Historical Window:** Analysis based on only 3 trading days
- **Static Classification:** Rules are fixed, not machine learning-based
- **Manual Updates:** Requires manual file refresh for new data
- **No Real-Time Data:** Not connected to live market feeds
- **Variance Coverage:** Limited to stocks with available variance data

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help improve this project:

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit your changes** (`git commit -m 'Add some AmazingFeature'`)
4. **Push to the branch** (`git push origin feature/AmazingFeature`)
5. **Open a Pull Request**

### Contribution Ideas

- 🔄 Add real-time NSE data integration
- 🤖 Implement ML-based categorization models
- 📊 Create interactive dashboards (Plotly/Dash)
- 🔧 Optimize performance for larger datasets
- 📚 Enhance documentation with video tutorials
- ✨ Add alert systems for category changes
- 🌐 Build web API for programmatic access
- 📱 Develop mobile app integration

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Aditya Singh**

[![GitHub](https://img.shields.io/badge/GitHub-AdiSinghCodes-181717?style=flat&logo=github)](https://github.com/AdiSinghCodes)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/aditya-singh)

### 📧 Contact

- **GitHub:** [@AdiSinghCodes](https://github.com/AdiSinghCodes)
- **LinkedIn:** [Aditya Singh](https://www.linkedin.com/in/aditya-singh)
- **Email:** Available on LinkedIn profile

### 💬 Feedback

- 🐛 **Found a bug?** [Open an issue](https://github.com/AdiSinghCodes/NSE-Stock-Categorization/issues)
- 💡 **Have a suggestion?** [Start a discussion](https://github.com/AdiSinghCodes/NSE-Stock-Categorization/discussions)
- 🤝 **Want to collaborate?** Connect on LinkedIn

---

## 🙏 Acknowledgments

- **NSE India** - For providing comprehensive and accessible market data
- **Pandas Development Team** - For the powerful data analysis library
- **Matplotlib & Seaborn Communities** - For excellent visualization tools
- **Open Source Community** - For continuous inspiration and support

---

## 🎯 Future Roadmap

- [ ] Real-time data integration via NSE API
- [ ] Machine learning-based categorization
- [ ] Interactive web dashboard (Streamlit/Dash)
- [ ] Historical trend analysis (multi-week/month)
- [ ] Automated alert system for category changes
- [ ] Portfolio optimization recommendations
- [ ] Risk assessment scoring system
- [ ] Mobile app for on-the-go access
- [ ] REST API for third-party integrations
- [ ] Backtesting framework for strategies

---

## 📚 Additional Resources

### Learning Materials
- [NSE India Official Website](https://www.nseindia.com/)
- [Python for Finance - Official Pandas Tutorial](https://pandas.pydata.org/docs/)
- [Data Visualization Best Practices](https://matplotlib.org/stable/tutorials/index.html)

### Related Projects
- Stock Market Analysis Tools
- Trading Strategy Backtesting Frameworks
- Portfolio Management Systems

### Documentation
- [Project Wiki](https://github.com/AdiSinghCodes/NSE-Stock-Categorization/wiki) (Coming Soon)
- [API Documentation](https://github.com/AdiSinghCodes/NSE-Stock-Categorization/docs) (Coming Soon)

---

## ⭐ Star History

If you find this project helpful, please consider giving it a star! It helps others discover the project and motivates continued development.

[![Star History Chart](https://api.star-history.com/svg?repos=AdiSinghCodes/NSE-Stock-Categorization&type=Date)](https://star-history.com/#AdiSinghCodes/NSE-Stock-Categorization&Date)

---

## 📊 Project Statistics

![GitHub repo size](https://img.shields.io/github/repo-size/AdiSinghCodes/NSE-Stock-Categorization)
![GitHub last commit](https://img.shields.io/github/last-commit/AdiSinghCodes/NSE-Stock-Categorization)
![GitHub issues](https://img.shields.io/github/issues/AdiSinghCodes/NSE-Stock-Categorization)
![GitHub pull requests](https://img.shields.io/github/issues-pr/AdiSinghCodes/NSE-Stock-Categorization)

---

<div align="center">

**Made with ❤️ by [Aditya Singh](https://github.com/AdiSinghCodes)**

*Last Updated: November 2024*

[⬆ Back to Top](#-nse-stock-categorization-system)

</div>
