
# SMD ScoreCard (Coming Soon)

## Synthetic Medical Data (SMD) Quality Library

A Python library for evaluating the quality of synthetic medical data (SMD) using the **7Cs framework** and for generating a comprehensive **SMD Card**. This library provides tools to compute quantitative metrics for dataset evaluation and document the results in a standardized card format.

---

## Features

### 7Cs Quality Evaluation
- Extract feature representation for quality quantification
- Compute metrics for:
  - **Congruence**: Measures the alignment between synthetic and real datasets to ensure structural, statistical, and visual similarity.
  - **Coverage**: Evaluates the diversity, representativeness, and novelty of the synthetic dataset. 
  - **Constraint**: Ensures that the synthetic data adheres to known constraints, which include clinical, imaging, geometric, or technical. 
  - **Completeness**: Checks whether synthetic data includes all necessary information (e.g., labels, metadata) required for its intended use.
  - **Compliance**: Assesses adherence to regulatory standards, fomrat, privacy, and institutional guidelines.
  - **Comprehension**: Evaluates the clarity and interpretability of the synthetic dataset's documentation.
  - **Consistency**: Ensures uniformity and stability of data quality across subgroups, batches, or time periods.

    
- Support for global and local quality assessments.

<br><br>

###  Library Metrics
The library contains a range of metrics summarized in the table below. Key attributes for each metric are described as follows:
- **Space**: Indicates the domain where the metric operates (e.g., embedding, metadata fields).
- **Binary**: Specifies whether the metric can be applied to synthetic data alone (unary) or requires comparison with patient data (binary).
- **Direction**: Describes the optimization goal (e.g., maximize, minimize, or statistical significance).
- **Image-Metric**: Indicates whether the metric is restricted to image or signal data or applicable to other types, such as clinical notes or numerical data.
- **Description**: Briefly explains what the metric evaluates and its relevance to SMD quality.

Note that the Direction of Coverage metrics should be maximized within a specific range to ensure synthetic medical data (SMD) is diverse while remaining valid and aligned with patient data.


| **Metric Example**             | **Space**          | **Binary?** | **Direction** | **Image Metric?** | **Description**                                                                 |
|---------------------------------|--------------------|-------------|---------------|--------------------|---------------------------------------------------------------------------------|
| **Congruence**                 |                    |             |               |                    |                         |
| Cosine Similarity              | Embedding          | Binary      | Maximize      | No                 | Measures alignment between feature vectors based on cosine distance.           |
| Earth Mover’s Distance         | Embedding          | Binary      | Minimize      | No                 | Quantifies the cost to transform one distribution into another.                |
| Jensen-Shannon Divergence      | Embedding          | Binary      | Minimize      | No                 | Measures similarity between probability distributions.                          |
| Peak Signal-to-Noise Ratio     | Image              | Binary      | Maximize      | Yes                | Evaluates image reconstruction quality by comparing signal-to-noise ratio.     |
| Structural Similarity Index    | Image              | Binary      | Maximize      | Yes                | Measures similarity between two images based on structure, luminance, and contrast. |
| Fréchet Inception Distance     | Embedding          | Binary      | Minimize      | Yes                | Evaluates distributional similarity of embeddings between datasets.            |
| Distance to Centroid           | Embedding          | Binary      | Minimize      | No                 | Measures how close feature vectors are to the cluster center.                  |
| Precision                      | Embedding          | Binary      | Maximize      | No                 | Assesses the proportion of true positives among predicted positives.           |
| **Coverage**                   |                    |             |               |                    |                 |
| Inception Score                | Image              | Unary       | Maximize      | Yes                | Evaluates image diversity and quality based on classification scores.          |
| Recall                         | Embedding          | Binary      | Maximize      | No                 | Measures the proportion of true positives among actual positives.              |
| Coverage                       | Embedding          | Binary      | Maximize      | No                 | Quantifies representation across subgroups or feature space.                   |
| Convex Hull Volume             | Embedding          | Unary       | Maximize      | No                 | Measures the occupied feature space volume of a dataset.                       |
| Variance                       | Embedding          | Unary       | Maximize      | No                 | Assesses variability in feature values.                                        |
| Entropy                        | Embedding          | Unary       | Maximize      | No                 | Quantifies randomness or uncertainty in feature distributions.                 |
| Rarity Score                   | Embedding          | Binary      | Minimize      | No                 | Evaluates the ability of synthetic data to capture rare patterns.              |
| Clustering-Based Metrics       | Embedding          | Unary       | Maximize      | No                 | Assesses how well data clusters in the feature space.                          |
| **Constraint**                 |                    |             |               |                    |             |
| Nearest Invalid Datapoint      | Embedding          | Binary      | Minimize      | No                 | Finds the closest point violating defined constraints.                         |
| Distance to Constraint Boundary| Embedding          | Binary      | Minimize      | No                 | Measures how close data points are to predefined constraint boundaries.         |
| Constraint Violation Rate      | Embedding          | Binary      | Minimize      | No                 | Calculates the proportion of data points violating constraints.                |
| **Completeness**               |                    |             |               |                    |                       |
| Proportion of Required Fields  | Metadata           | Binary      | Maximize      | No                 | Assesses the percentage of mandatory fields filled in the dataset.             |
| Missing Data Percentage        | Metadata           | Binary      | Minimize      | No                 | Quantifies the percentage of missing entries in the dataset.                   |
| **Compliance**                 |                    |             |               |                    | 
| Differential Privacy Score     | Data Attribute     | Unary       | Minimize      | No                 | Quantifies privacy guarantees using a differential privacy parameter (𝜀).      |
| K-Anonymity Level              | Data Attribute     | Unary       | Maximize      | No                 | Ensures that each individual is indistinguishable within a group of size \( k \). |
| L-Diversity Score              | Data Attribute     | Unary       | Maximize      | No                 | Measures diversity within groups to prevent attribute-based identification.     |
| T-Closeness Level              | Data Attribute     | Unary       | Maximize      | No                 | Assesses how close attribute distributions are within groups.                  |
| **Comprehension**              |                    |             |               |                    |                   |
| Documentation Clarity Score    | Documentation      | Unary       | Maximize      | No                 | Measures the clarity and usability of accompanying documentation.              |
| **Consistency**                |                    |             |               |                    |                        |
| Variance                       | Quality Metrics    | Unary       | Minimize      | No                 | Evaluates variability in quality metrics across groups.                        |
| Maximum-Minimum Difference     | Quality Metrics    | Unary       | Minimize      | No                 | Calculates the range of quality metrics across subgroups.                      |
| Analysis of Variance           | Quality Metrics    | Unary       | Stat. Sig.    | No                 | Tests statistical significance of quality variations across subgroups.         |


 
### Flexible Input Types
- Analyze image datasets or embeddings.
- Tailor metrics to specific criteria and constraints.

### SMD Card Generation
- Automatically generate a JSON-formatted card summarizing dataset quality.
- Document:
  - General information
  - Quantitative results
  - Task performance
  - Ethical considerations

### Extensibility
- Add custom metrics for specific evaluation needs.
- Adapt the card to fit diverse applications and regulatory contexts.
