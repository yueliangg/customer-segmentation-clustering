# Customer Segmentation using Unsupervised Learning

Segmenting 200 shopping-mall customers into actionable groups based on age, income and spending behaviour, using K-Means and Hierarchical clustering.

**Final model:** K-Means (k = 6), silhouette score 0.443, outperforming Agglomerative (Ward) clustering on all three internal validation metrics.

---

## Problem Overview

| | |
|---|---|
| **Task** | Unsupervised learning (clustering) |
| **Dataset** | `CA2-Customer-Data.csv`: 200 customers, 5 columns |
| **Features used** | Age, Annual Income (k$), Spending Score (1–99) |
| **Goal** | Identify distinct customer segments to support targeted marketing |

Since there are no labels, the models are evaluated with internal clustering metrics (Silhouette, Davies-Bouldin and Calinski-Harabasz) and judged on how interpretable the segments are for the business.

---

## Tech Stack

Python, pandas, NumPy, scikit-learn, SciPy, Matplotlib, Seaborn, Jupyter Notebook

---

## Workflow

1. **Exploratory Data Analysis:** distributions, gender balance, pairwise relationships and outlier detection.
2. **Preprocessing:**
   - Income capped at the 95th percentile ($103k) to reduce the influence of high earners
   - `CustomerID` removed
   - Min-Max scaling applied inside an sklearn `Pipeline`
3. **Choosing k:** elbow method, silhouette analysis for k = 2 to 10, and dendrogram inspection.
4. **Modelling:** K-Means and Agglomerative Clustering (Ward linkage), compared at k = 6.
5. **Evaluation:** Silhouette, Davies-Bouldin and Calinski-Harabasz scores, plus a 2D PCA visualisation (78% of variance explained).
6. **Interpretation:** segment profiling, per-cluster silhouette analysis and business recommendations.

---

## Results

### Model Comparison (k = 6)

| Metric | K-Means | Hierarchical | Better |
|---|---|---|---|
| Silhouette (higher is better) | **0.443** | 0.433 | K-Means |
| Davies-Bouldin (lower is better) | **0.806** | 0.831 | K-Means |
| Calinski-Harabasz (higher is better) | **149.04** | 132.73 | K-Means |

### Customer Segments

| Segment | Share | Avg Age | Avg Income | Avg Spending | Silhouette |
|---|---|---|---|---|---|
| Premium Customers | 19.5% | 32.7 | $86.5k | 82.1 | 0.549 |
| Young Big Spenders | 12.0% | 25.2 | $25.8k | 76.9 | 0.501 |
| Wealthy Savers | 16.5% | 41.9 | $88.9k | 17.0 | 0.379 |
| Mature Moderate Spenders | 22.5% | 56.3 | $54.3k | 49.1 | 0.481 |
| Young Moderate Spenders | 19.0% | 26.7 | $57.6k | 47.8 | 0.381 |
| Budget Shoppers | 10.5% | 45.5 | $26.3k | 19.4 | 0.312 |

---

## Key Insights

- **Income does not determine spending.** The two high-income segments behave in opposite ways: Premium Customers average a spending score of 82, while Wealthy Savers average only 17.
- **High spenders are young.** Both high-spending segments have an average age under 33.
- **Wealthy Savers are the largest untapped opportunity.** They have the highest average income of any segment but one of the lowest spending scores.
- **Gender has little effect.** Every segment is between 42% and 63% female, so gender was used for profiling only, not for clustering.

---

## Business Recommendations

| Priority | Segment | Recommended Action |
|---|---|---|
| Retain | Premium Customers | VIP or loyalty tier, early access, personalised service |
| Grow | Wealthy Savers | Premium-quality and value messaging, exclusive events |
| Engage | Young Big Spenders | Trend-led promotions and social media campaigns |
| Upsell | Young Moderate Spenders | Bundles and loyalty points to build towards the premium segment |
| Maintain | Mature Moderate Spenders | Loyalty programme and reliable, quality-focused service |
| Cost-efficient | Budget Shoppers | Discounts and value packs, with low marketing spend |

---

## Repository Structure

```
├── customer_segmentation.ipynb          # Full analysis notebook
├── CA2_PartA_Customer_Segmentation.pptx # Presentation slides
├── data/
│   └── CA2-Customer-Data.csv
└── README.md
```

---

## How to Run

```bash
git clone <this-repo-url>
cd <repo-folder>
pip install pandas numpy scikit-learn scipy matplotlib seaborn
jupyter notebook customer_segmentation.ipynb
```

Set the dataset path in the loading cell:

```python
df_raw = pd.read_csv("data/CA2-Customer-Data.csv")
```

Then select **Kernel > Restart & Run All**. Results are reproducible (`random_state=42`).

---

## Limitations and Future Work

- A silhouette score of 0.44 indicates moderate separation, so some customers sit between neighbouring segments.
- The dataset is small (200 customers, 3 features). Adding purchase history or visit frequency would allow more precise targeting.
- Density-based methods such as DBSCAN could be tested to detect irregularly shaped clusters.

---

## Author

**Thawdar Lin Wai**
Diploma in Applied AI and Analytics, Singapore Polytechnic
