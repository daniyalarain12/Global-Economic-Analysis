# 🌍 Global Economic Analysis — World Bank Data (2010–2025)

![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-1.x-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-orange?style=for-the-badge&logo=python&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13.x-4C72B0?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

> A complete Exploratory Data Analysis on World Bank economic data covering 217 countries from 2010 to 2025 — uncovering GDP trends, inflation patterns, unemployment insights, COVID-19 economic impact and economy size distribution using Python, Pandas, Matplotlib and Seaborn.

---

## 📁 Repository Structure

```
Global-Economic-Analysis/
│
├── Global_Economic_Analysis.ipynb
├── world_bank_data_2025.csv
└── README.md
```

---

## 📂 Dataset

| Detail | Info |
|--------|------|
| **File** | world_bank_data_2025.csv |
| **Source** | [World Bank — Global Economic Indicators](https://www.worldbank.org) |
| **Rows** | 3,472 |
| **Countries** | 217 |
| **Year Range** | 2010 – 2025 |

### Key Columns

| Column | Description |
|--------|-------------|
| `country_name` | Country name |
| `year` | Year (2010–2025) |
| `GDP (Current USD)` | Total GDP in US Dollars |
| `GDP per Capita (Current USD)` | GDP per person |
| `GDP Growth (% Annual)` | Annual GDP growth rate |
| `Inflation (CPI %)` | Consumer Price Index inflation |
| `Inflation (GDP Deflator, %)` | Broader inflation measure |
| `Unemployment Rate (%)` | Unemployment percentage |
| `Gross National Income (USD)` | Total national income |
| `Current Account Balance (% GDP)` | Trade balance |

---

## 🧹 Data Cleaning

| Step | Action |
|------|--------|
| Dropped 6 columns | `country_id`, `Public Debt`, `Interest Rate`, `Govt Expense`, `Govt Revenue`, `Tax Revenue` — over 40% missing |
| GDP Growth nulls | Filled with **0** — no growth is safer assumption than median for rate columns |
| All other nulls | Filled with **country-specific median** using `groupby + map` — most meaningful approach |
| Fallback fill | Remaining nulls filled with **global median** — handles countries with all values missing |
| New column | `economy_size` — created using custom Python function + `apply()` |

### Economy Size Classification

| Category | GDP Range |
|----------|-----------|
| **MEGA** | GDP ≥ $1 Trillion |
| **LARGE** | GDP $100B – $1T |
| **MEDIUM** | GDP $10B – $100B |
| **SMALL** | GDP < $10 Billion |

---

## 📊 Analyses Performed

| # | Analysis | Chart Type | Key Question |
|---|----------|------------|-------------|
| 01 | Top 10 Largest Economies | Horizontal Bar | Which countries have the biggest total economies? |
| 02 | Top 10 GDP per Capita | Horizontal Bar | Which countries are wealthiest per person? |
| 03 | Average GDP Trend | Line Plot | How has the average economy size grown over time? |
| 04 | Global GDP Growth Rate | Line Plot + axhline | When did the global economy crash — and how fast did it recover? |
| 05 | Global Inflation Trend | Line Plot + axhline | When did inflation spiral — is it back under control? |
| 06 | Economy Size Distribution | Pie Chart | How many countries have trillion dollar economies? |
| 07 | Unemployment vs GDP Growth | Scatter Plot | Do high unemployment countries have lower growth? |
| 08 | Top 10 Unemployment Countries | Vertical Bar | Which countries have the worst unemployment crisis? |
| 09 | Inflation Rate Distribution | Histogram + axvlines | What inflation rate is most common globally? |
| 10 | GDP Growth by Economy Size | Box Plot | Are smaller economies more volatile than larger ones? |
| 11 | GDP vs GDP per Capita | Scatter Plot with hue | Can small economies have high per capita wealth? |
| 12 | Inflation Comparison — 6 Countries | Seaborn lineplot | Did all countries suffer equally from post-COVID inflation? |
| 13 | GDP Growth Heatmap | Seaborn Heatmap + Pivot | Which country crashed hardest in 2020 — who recovered fastest? |
| 14 | GDP Stack Plot — 6 Economies | Stack Plot | How has the combined GDP of major economies grown? |
| 15 | Final Dashboard | 3x2 Subplots | Complete global economic picture at a glance |

---

## 🔑 Key Insights

- **USA and China** dominate global GDP — their combined economy dwarfs all others
- **Small nations** like Luxembourg and Singapore have far higher GDP per capita than large economies
- **COVID-19 in 2020** caused the worst global economic contraction since 2010 — visible as a dramatic dip across all analyses
- **Post-COVID inflation (2021–2022)** spiked to the highest levels in the entire dataset — far above the 2% healthy target
- **Higher cholesterol countries** — wait, that was another project 😄 — Higher inflation countries tend to have more volatile GDP growth
- **SMALL economies** show significantly more GDP growth volatility than MEGA economies — confirmed by box plot
- **Pakistan** showed surprising resilience in certain years compared to regional peers

---

## 🗺️ Countries Analyzed in Depth

| Country | Region | Why Selected |
|---------|--------|-------------|
| United States | North America | World's largest economy |
| China | Asia | World's fastest growing mega economy |
| Germany | Europe | Largest European economy |
| India | South Asia | World's most populous economy |
| Brazil | South America | Largest Latin American economy |
| Pakistan | South Asia | Personal relevance + emerging market |

---

## 🛠️ Tech Stack

| Library | Purpose |
|---------|---------|
| **Pandas** | Data loading, cleaning, groupby, pivot and transformation |
| **NumPy** — | Numerical operations |
| **Matplotlib** | Bar, line, scatter, pie, histogram, stack plot and subplots |
| **Seaborn** | Lineplot, scatter with hue, box plot and heatmap |

---

## 💡 Most Innovative Code — Smart fillna

Instead of filling each column separately — all 8 columns filled in **one single `fillna()` call** with country-specific medians:

```python
data = df.groupby('country_name')
df.fillna({
    'GDP Growth (% Annual)' : 0,
    'Inflation (CPI %)'     : df['country_name'].map(data['Inflation (CPI %)'].median()),
    'Unemployment Rate (%)'  : df['country_name'].map(data['Unemployment Rate (%)'].median()),
    # ... all columns in one call
}, inplace=True)
```

---

## ▶️ How to Run

1. Clone the repository
```bash
git clone https://github.com/daniyalarain12/Global-Economic-Analysis.git
```

2. Install required libraries
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

3. Launch Jupyter Notebook
```bash
jupyter notebook
```

4. Open `Global_Economic_Analysis.ipynb` and run all cells

---

## 🗺️ My Data Science Learning Journey

This is my final EDA project before starting Machine Learning:

| Repository | Status |
|-----------|--------|
| [Python — Basics to Advanced](https://github.com/daniyalarain12/Python-Basics-to-Advanced) | ✅ Completed |
| [NumPy — Basics to Advanced](https://github.com/daniyalarain12/NumPy-Basics-To-Advanced) | ✅ Completed |
| [Pandas — Basics to Advanced](https://github.com/daniyalarain12/Pandas-Basics-to-Advanced) | ✅ Completed |
| [Matplotlib — Basics to Advanced](https://github.com/daniyalarain12/Matplotlib-Basics-to-Advanced) | ✅ Completed |
| [Netflix EDA — Project](https://github.com/daniyalarain12/Netflix-EDA-Visualization) | ✅ Completed |
| [Seaborn — Basics to Advanced](https://github.com/daniyalarain12/Seaborn-Basics-to-Advanced) | ✅ Completed |
| [IPL Data Analysis — Project](https://github.com/daniyalarain12/IPL-Data-Analysis) | ✅ Completed |
| [Cardiovascular Disease EDA — Project](https://github.com/daniyalarain12/Cardiovascular-Disease-EDA) | ✅ Completed |
| **Global Economic Analysis — Project** | ✅ Completed |
| Machine Learning | 🔜 Starting Now 🚀 |

---

## 📬 Connect With Me

[![GitHub](https://img.shields.io/badge/GitHub-daniyalarain12-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/daniyalarain12)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/daniyal-arain)

---

⭐ **If you find this repository helpful, please give it a star!** ⭐
