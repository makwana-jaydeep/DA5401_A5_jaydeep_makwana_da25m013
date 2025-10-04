# DA5401 A5: Visualizing Data Veracity Challenges in Multi-Label Classification


**NAME : Jaydeep Makwana** 

**Roll Number : DA25M013**
## 1. Executive Summary
This project applies **non-linear dimensionality reduction techniques** — *t-SNE* and *Isomap* — to the **Yeast Gene Expression Dataset** to visually examine critical **data veracity challenges**.  

The analysis reveals:
- **Noisy and ambiguous labels**
- **Complex, curved data manifolds**
- **Hard-to-separate clusters**

These findings explain why conventional machine learning models perform poorly on this **multi-label classification** problem.  
The visualizations provide clear, empirical evidence of the dataset’s underlying complexity and manifold structure.

---

## 2. Methodology and Implementation

### 2.1 Data Preprocessing and Scaling
**Feature Scaling:**  
All 103 gene expression features (`X`) were standardized using `StandardScaler` to ensure each had a mean of 0 and standard deviation of 1.  
This step is essential because both *t-SNE* and *Isomap* are sensitive to feature magnitudes.

**Label Simplification:**  
The original 14 binary class indicators were aggregated into four high-level categories for meaningful visualization:

| Category | Description |
|-----------|--------------|
| **L1** | Top Single-Label Class (`Class1`) |
| **C1** | Most frequent multi-label combination |
| **C2** | Second most frequent multi-label combination |
| **Other** | All remaining single and multi-label samples |

**Rationale for Adaptation:**  
The dataset contains only one single-label class (`Class1`). Therefore, the second single-label class (`L2`) was replaced with the second most frequent multi-label combination (`C2`) to maintain four distinct, interpretable color groups in the visualization.

---

### 2.2 Dimensionality Reduction
| Technique | Focus | Key Parameter | Rationale |
|------------|--------|----------------|------------|
| **t-SNE (t-Distributed Stochastic Neighbor Embedding)** | Local structure (clustering) | `perplexity = 30` | After testing perplexities (5, 30, 50), 30 provided the clearest separation with minimal artificial fragmentation. |
| **Isomap (Isometric Mapping)** | Global structure (manifold shape) | `n_neighbors = 10` | Preserves geodesic distances, effectively revealing the global topology of the data manifold. |

---

## 3. Results and Veracity Inspection

### 3.1 t-SNE: Inspection of Local Cluster Integrity
Key findings from the t-SNE visualization:

- **Noisy/Ambiguous Labels:**  
  Samples labeled as one class (e.g., L1 or C2) were often embedded within another dominant cluster (e.g., C1), indicating label overlap or ambiguous biological functions.

- **Hard-to-Learn Samples:**  
  Mixed regions containing all four color categories suggest overlapping feature spaces and highly non-linear decision boundaries.

- **Outliers:**  
  Distant “Other” samples represent rare or anomalous gene expression patterns — possibly measurement noise or unique biological states.

---

### 3.2 Isomap: Manifold Complexity Analysis
Key observations from Isomap visualization:

- **Global Structure Preservation:**  
  Clusters appear stretched and interconnected, confirming Isomap’s strength in maintaining global geometric relationships.

- **Manifold Complexity:**  
  The Isomap projection reveals a **curved, non-linear manifold**, indicating that the data cannot be represented accurately using linear assumptions.

- **Classification Implications:**  
  The curved structure explains why **linear models (e.g., Logistic Regression)** fail, and supports the need for **non-linear classifiers** (e.g., SVM with RBF kernel, Random Forests, Neural Networks).

---

## 4. Conclusion
The visual analysis using **t-SNE** and **Isomap** confirms that the **Yeast Gene Expression Dataset** exhibits substantial challenges in **data veracity** and **structural complexity**:

- Labels are noisy and ambiguous.  
- The data manifold is non-linear and highly curved.  
- Classification boundaries are inherently complex.

These findings justify the use of **robust, non-linear machine learning methods** and emphasize the intrinsic difficulty of classifying **multi-functional biological entities** based solely on gene expression data.

---

##  Project Files
- `yeast.csv` — Main dataset  
- `visualization.ipynb` — Notebook containing preprocessing, t-SNE, and Isomap analysis  
- `README.md` — Project documentation  
---

##  Requirements
```bash
pip install pandas numpy seaborn matplotlib scikit-learn 

