# Behavioral and Sentiment Divergence Across Mobile Platform Ecosystems: A Large-Scale Analysis of Amazon Reviews

**Sam El Saati · Mohamad Alloush**  
BSc Big Data Analytics Project (DA381A) — Kristianstad University (HKR)  
Supervisor: Dr. Ali Sodhro · Grade: Distinction

---

## Research Question

Do iOS and Android users exhibit measurably different behavioral and sentiment patterns in product reviews, and if so, what does the divergence reveal about platform-specific consumption culture?

This question matters beyond the iOS/Android frame. User-generated review data is one of the largest sources of unsolicited behavioral signal available online. Understanding how to extract coherent behavioral patterns from noisy, unstructured, large-scale text corpora is a methodological challenge with broad applicability — to health technology adoption, civic platforms, and consumer behavior research.

---

## Dataset

**Amazon Reviews 2023 — Cell Phones and Accessories**  
Source: [McAuley-Lab/Amazon-Reviews-2023](https://huggingface.co/datasets/McAuley-Lab/Amazon-Reviews-2023)  
Size: ~9GB  
Format: JSON, ingested via HDFS

The dataset includes review text, ratings, timestamps, and product metadata for mobile phone accessories — a domain with clear platform segmentation between iOS-compatible and Android-compatible products.

---

## Method

**Infrastructure:** Hadoop HDFS (distributed storage) + Apache PySpark (distributed processing). Pandas and Matplotlib for downstream aggregation and visualization.

The pipeline runs in four stages:

1. **Ingestion and storage** — Raw JSON loaded into HDFS. The 9GB scale required optimized HDFS block configuration to avoid memory exhaustion during initial load.

2. **Preprocessing** — JSON-to-CSV conversion, missing value handling, outlier removal, timestamp validation. Platform categorization was derived from product metadata and review keywords.

3. **Feature engineering** — Sentiment labels (positive / neutral / negative) assigned using a classification approach applied to review text. Platform category (iOS / Android) assigned per review.

4. **Analysis** — Comparative behavioral analysis across platform cohorts: sentiment distribution, keyword frequency, temporal trend extraction. Word clouds generated per platform to surface dominant semantic themes.

**Engineering note:** The dataset size pushed against memory limits of the available compute environment. A non-trivial portion of the project was spent on system configuration — tuning HDFS block sizes, PySpark executor memory allocation, and processing partitioning — to run the full pipeline without crashes. These optimizations are documented in the notebook.

---

## Findings

iOS-associated reviews cluster around aesthetic and brand-related language — keywords including *"perfect," "fit," "Apple"* dominate the word cloud. Android-associated reviews cluster around functional and value-oriented language — *"battery," "Samsung," "work"* are the dominant signals.

Sentiment distributions differ between cohorts: iOS reviews show a higher proportion of strongly positive sentiment, while Android reviews are more uniformly distributed across sentiment categories. Temporal analysis suggests iOS sentiment correlates with product release cycles more than Android sentiment does.

These findings are consistent with prior work on platform-based consumer identity and purchase motivation, though the scale of the dataset (9GB, multi-year) allows finer-grained temporal analysis than most prior studies using smaller scraped corpora.

---

## Reproducibility

```bash
git clone https://github.com/sams258/Big-Data-Analytics-Project
```

Dependencies: Hadoop, PySpark, Pandas, Matplotlib. Full setup instructions and Jupyter notebook in the repository. Requires HDFS configuration tuning for datasets above ~5GB — see notebook comments.

---

## References

- Hadoop Documentation: https://hadoop.apache.org/docs/stable/
- PySpark Quick Start: https://spark.apache.org/docs/latest/quick-start.html
- Pandas Documentation: https://pandas.pydata.org/docs/
- Dataset: https://huggingface.co/datasets/McAuley-Lab/Amazon-Reviews-2023
