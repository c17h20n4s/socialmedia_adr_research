# Social-Media Pharmacovigilance Analysis
### Using Reddit dataset for Adverse Drug Reaction (ADR) Clusters and Symptom Embeddings

## Overview
This project investigates adverse drug reactions (ADRs) reported by Reddit users and constructs a data-driven pharmacovigilance knowledge map. Using graph analytics and unsupervised machine learning, the pipeline identifies co-occurring symptoms, clusters, and embedding-based similarities between ADRs—aligned with limited MedDRA-style medical taxonomy.

## Objectives
- Extract and clean Reddit-based ADR data.  
- Build a co-occurrence network to reveal symptom relationships.  
- Apply community detection to discover syndrome-like clusters.  
- Train Word2Vec (contextual) and Node2Vec (structural) embeddings for similarity modeling.  
- Visualize ADR embeddings interactively and map them to System Organ Classes (SOC).

## Pipeline Summary
| Stage | Notebook | Key Output | Description |
|--------|-----------|-------------|--------------|
| **1. Data Preprocessing** | `01_pre_processing_pipeline.ipynb` | `reddit_adr_clean.csv`, `fig_top_adrs.png` | Cleans raw Reddit data and computes frequency distributions. |
| **2. Network & Clustering** | `02_network_and_clustering_ADR.ipynb` | `adr_network_filtered_cutoff_2.gml`, `fig_adr_heatmap_cutoff_2.png` | Builds symptom co-occurrence network and detects communities. |
| **3. Embeddings Analysis** | `03_embeddings_analysis.ipynb` | `w2v_adr.model`, `node2vec_adr.model`, `fig_embeddings_tsne.png` | Learns contextual (Word2Vec) and structural (Node2Vec) ADR embeddings. |
| **4. Visualization & MedDRA Mapping** | `04_visualizations_and_medra.ipynb` | `adr_embeddings_labeled_cutoff_2.csv`, `fig_embeddings_soc_cutoff_2.html` | Integrates embeddings with pseudo-MedDRA taxonomy and interactive visualization. |

## Data
- **Source:** Synthetic Reddit ADR dataset.  
  Each record contains a `post_id` (user) and one ADR term.  
- **Scale:** Approximately 1,400 ADR mentions and 200 unique symptom terms.  
- **Processing:** Cleaned, lowercased, deduplicated, and aggregated per user.

## Methods
| Method | Description |
|--------|--------------|
| Network Analysis | Built co-occurrence graph using `networkx`; filtered edges ≥2 shared users. |
| Community Detection | Applied greedy modularity optimization to identify ADR clusters. |
| Word2Vec | Learned contextual ADR relationships from user-level “symptom sentences.” |
| Node2Vec | Captured structural similarity in the co-occurrence graph topology. |
| Dimensionality Reduction | Used t-SNE for 2D visualization of the embedding space. |
| MedDRA Mapping | Assigned each ADR to a pseudo System Organ Class (SOC) hierarchy for interpretability. |

## Key Findings
| Insight | Example |
|----------|----------|
| Cluster 1 | Withdrawal, Depression, Panic Attacks, Tremors, Cravings to Psychiatric Disorders / Dependence Syndrome |
| Cluster 2 | Anxiety, Derealization, Tinnitus, Numbness to Nervous System Disorders |
| Cluster 3 | Insomnia, Fatigue, Sweating, Exhaustion to Sleep and Fatigue Syndromes |
| Cluster 4 | Nausea, Dizziness, Vomiting, Diarrhea to Gastrointestinal Disorders |
| Bridge Symptoms | Fatigue, Anxiety, Headache act as connectors across clusters. |

## Visualizations
- Top 40 Reported ADRs — frequency bar plot.  
- Co-occurrence Heatmap — correlation of ADR co-reporting.  
- Filtered Network Graph — community-colored visualization.  
- t-SNE Embedding Map — 2D projection of Node2Vec symptom embeddings.  
- Symptom Similarity Map — normalized co-occurrence intensity.  
- SOC-Labeled Interactive Map — Plotly visualization colored by System Organ Class.

## Technologies
| Category | Tools |
|-----------|-------|
| Data processing | pandas, numpy |
| Network analysis | networkx, community |
| NLP embeddings | gensim, node2vec |
| Visualization | matplotlib, seaborn, plotly, dash |
| ML utilities | scikit-learn, t-SNE, Word2Vec |

## Repository Structure

socialmedia_adr_research/
├── data/
│ ├── raw/
│ ├── processed/
├── models/
│ ├── node2vec/
│ ├── word2vec/
├── notebooks/
│ ├── pre_processing_pipeline.ipynb
│ ├── network_and_clustering_ADR.ipynb
│ ├── embeddings_analysis.ipynb
│ └── visualizations_and_medra.ipynb
├── src/ # to be added
│ ├── data_utils.py 
│ ├── network_utils.py
│ ├── embedding_utils.py
│ └── viz_utils.py
├── README.md
└── requirements.txt


## Key Metrics
| Metric | Result |
|--------|---------|
| Unique ADRs | 667 |
| Unique Users (posts) | 600 |
| Communities Detected | 7 |
| Adjusted Rand Index (Cluster ↔ SOC) | ≈ 0.4 |
| Embedding Dimension | 64 |
| Visualization Reduction | t-SNE (perplexity = 20) |

## Interpretation
The network analysis revealed clear clusters of co-occurring symptoms consistent with psychiatric, neurological, and gastrointestinal domains.  
Node2Vec embeddings showed that structurally similar ADRs (e.g., withdrawal, anxiety, insomnia) are close in vector space, providing an interpretable map of symptom relationships.  
This demonstrates how social-media data can approximate pharmacovigilance structures such as MedDRA System Organ Classes.

## Next Steps
- Integrate association-rule mining (Apriori) to predict next-likely ADRs.  
- Add temporal component for longitudinal symptom analysis.  
- Compare to real MedDRA or FAERS data for validation.  
- Deploy interactive Dash dashboard for public demo.

## Author
Polina Pshonkovskaya  
Neuroscientist & Applied Machine Learning Scientist  
LinkedIn: https://www.linkedin.com/in/polina-p-361885130/ 


## Citation
Pshonkovskaya, P. (2025). *Social-Media Pharmacovigilance Assistant: Reddit dataset for ADR Clusters and Symptom Embeddings.*
