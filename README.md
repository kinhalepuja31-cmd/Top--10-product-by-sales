# Top--10-product-by-sales

## 📊 Project Overview
The goal of this assignment is to process multi-sheet sales records, perform transactional aggregation, resolve statistical data ties seamlessly, and generate presentation-ready business visualizations.

### Key Deliverables:
1. **Multi-Sheet Extraction:** Reading targeted transactional data (`Orders`) directly from a multi-file Excel sheet.
2. **Data Aggregation & Grouping:** Isolating individual product revenue performance.
3. **Competition-Grade Ranking:** Implementing robust tie-breaking mechanics via `pandas.Series.rank(method='min')`.
4. **Data Visualization:** Producing a clean, horizontal comparative bar plot using Seaborn.

## 🛠️ Tech Stack & Libraries
* **Environment:** Google Colab / Jupyter Notebooks
* **Language:** Python 3.x
* **Core Data Engine:** `pandas`
* **Visualization Suite:** `matplotlib` & `seaborn`

## 🚀 Step-by-Step Implementation Workflow

### 1. Load Environment & Dataset
The process begins by importing dependencies and parsing the specific `Orders` sheet layout out of the multi-file workbook uploaded to the local notebook storage path (`/content/Global Superstore Data.xlsx`).

python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load only the required sheet layer
df = pd.read_excel('/content/Global Superstore Data.xlsx', sheet_name='Orders')

# Preview structural rows
df.head()

### 2. Grouping and Aggregation
Individual transactions are summed globally across every distinct product description identifier.
python
# Group data by Product Name and calculate total sales volume
product_sales = df.groupby('Product Name')['Sales'].sum().reset_index()

### 3. Sorting & Checking for Ties (Ranking Logic)
To maintain structural compliance for overlapping financial milestones, data rows are ordered descending, and the `min` evaluation method is enforced to guarantee tied entries receive standard identical placement values without skip distortions.
python
# Sort descending by Sales
product_sales = product_sales.sort_values(by='Sales', ascending=False).reset_index(drop=True)

# Assign ranks handling ties (method='min' ensures tied rows map to identical placements)
product_sales['Rank'] = product_sales['Sales'].rank(ascending=False, method='min').astype(int)

# Isolate top tier boundaries
top_10_products = product_sales[product_sales['Rank'] <= 10]

### 4. Chart Visualization Deliverable
A horizontal layout prevents character clipping on descriptive product inventory descriptions while visually communicating financial weight categories using a standardized `viridis` spectrum.
python
plt.figure(figsize=(10, 6))
sns.set_theme(style="whitegrid")

# Create a horizontal bar plot 
# Note: Assigning 'hue' maps directly to standard Seaborn requirements to prevent deprecation adjustments
sns.barplot(
    x='Sales', 
    y='Product Name', 
    data=top_10_products, 
    hue='Product Name',
    palette='viridis',
    legend=False
)

plt.title('Top 10 Products by Total Sales', fontsize=14, fontweight='bold', pad=15)
plt.xlabel('Total Sales (\$)', fontsize=12)
plt.ylabel('Product Name', fontsize=12)

plt.tight_layout()
plt.show()
## 📈 Analysis Insights & Key Findings
* **Top Revenue Generator:** The **Apple Smart Phone, Full Size** commands the top position in total performance output volume.
* **Tie Verification:** Implementing competition ranking ensures that if multiple high-profile entries achieve identical decimal thresholds on final cutoffs, they remain completely cataloged without causing index-truncation loss.
* **Visual Optimization:** Applying horizontal axis projections delivers an optimal layout for viewing lengthy operational inventory strings (e.g., *Office Star Executive Leather Armchair, Adjustable*).
