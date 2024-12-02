# SMD ScoreCard (Coming Soon)

## Synthetic Medical Data (SMD) Quality Library

A Python library for evaluating the quality of synthetic medical data (SMD) using the **7Cs framework** and for generating a comprehensive **SMD Card**. This library provides tools to compute quantitative metrics for dataset evaluation and document the results in a standardized card format.

---

## Index

- [Overview](#overview)
- [Installation](#installation)
- [Key Features](#key-features)
  - [Feature Extraction](#feature-extraction)
  - [Quality Quantification](#quality-quantification)
  - [Aggregated Score Computation](#aggregated-score-computation)
  - [SMD Card Generation](#smd-card-generation)
- [Flexible Input Types](#flexible-input-types)
- [Extensibility](#extensibility)

---

## Overview

The **SMD ScoreCard** library provides a structured framework for evaluating the quality of synthetic medical datasets. Leveraging the **7Cs framework**, the library helps researchers and developers assess critical aspects of synthetic datasets, including correctness, coverage, constraints, and compliance. Additionally, it offers tools for feature extraction, quality quantification, and documentation, ensuring that datasets meet clinical, technical, and regulatory standards.

---

## Installation

### Prerequisites

Ensure that you have Python 3.8 or higher installed on your system. 

### Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/smd-scorecard.git
   cd smd-scorecard

2. **Install Required Packages**
   Use the requirements.txt file to install dependencies:
   ```bash
   pip install -r requirements.txt

3. **Verify Installation**
   Run the following command to check if the library is correctly installed:
   ```bash
   python -m smd_scorecard --help

   
--- 
## Key Features

### Feature Extraction

The library includes a **Feature Extraction Module** to extract meaningful representations from data, including:

- **Token Embeddings**: Extract features from clinical notes or textual data to enable semantic analysis.
- **Imaging Features**: Extract spatial, intensity, or structural properties from medical images using radiomic or deep learning-based embeddings.
- **Feature Summarization**: Summarize high-dimensional feature spaces to compact representations using techniques like dimensionality reduction or statistical summarization.

---

### Quality Quantification

The second step involves **quantification based on the 7Cs framework**, which evaluates SMD across key quality dimensions:

1. **Congruence**: Measures alignment between synthetic and real data.
2. **Coverage**: Evaluates diversity, representativeness, and novelty.
3. **Constraint**: Ensures adherence to known constraints, including clinical, imaging, and technical.
4. **Completeness**: Assesses whether all necessary information (e.g., labels, metadata) is included.
5. **Compliance**: Verifies adherence to regulatory standards, privacy, and format guidelines.
6. **Comprehension**: Evaluates clarity and interpretability of accompanying documentation.
7. **Consistency**: Ensures uniformity of quality across subgroups, batches, or time periods.

###  Quantification Metrics
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

---
### Aggregated Score Computation

The library provides a module for computing an **aggregated quality score** based on:

- **Normalized Averaging**: Averages metrics across criteria to generate a composite score.
- **Geometric Mean**: Aggregates metrics to reflect trade-offs between different quality aspects.

---

### SMD Card Generation

The library includes a **SMD Card Tool** to assist researchers in documenting and summarizing their datasets. This tool enables:

- **Standardized Reporting**: Generates a JSON-formatted card summarizing:
  - General dataset information
  - Synthetic Data Quality (Quantitative)
  - Task-specific performance metrics (Quantitative)
  - Human-based Evaluation (Qualitative)
  - Ethical considerations and limitations
  - Synthetic Dataset Usage
  - Synthetic Dataset Training & Validation Process
  - Reference Dataset General Information
- **Customizable Templates**: Tailor the SMD Card to specific regulatory or research requirements.

  ![Sinkove Synthetic CSAW 100k Mammograms - DIDSR ScoreCard_Page_1](https://github.com/user-attachments/assets/c8d3ade2-f509-407f-84bc-2190a3dfd382)


---

## Flexible Input Types

The library supports:

- **Image Datasets**: Analyze medical images using radiomic and deep features.
- **Token Embeddings**: Evaluate clinical notes or textual datasets.
- **Tabular Data**: Apply quality metrics to numerical datasets.

---

## Extensibility

The **SMD ScoreCard** library is designed to be adaptable:

- **Add Custom Metrics**: Extend the library by defining metrics specific to your evaluation needs.
- **Customize the SMD Card**: Modify templates to align with clinical, regulatory, or application-specific contexts.
- **Support for Diverse Modalities**: Expand feature extraction capabilities to additional data types (e.g., genomic data, signals).

This library aims to simplify and standardize the evaluation of synthetic datasets, ensuring that they are robust, reliable, and suitable for their intended applications.


---

## License

This project is licensed under the **MIT License**. 

### Summary of the MIT License:
- You are free to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of this software, provided that the above copyright notice and this permission notice are included in all copies or substantial portions of the software.
- The software is provided "as-is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement.

For full details, see the [LICENSE](LICENSE) file included in this repository.

---.

If you use this library in your research, please consider citing it or contributing to its development!
