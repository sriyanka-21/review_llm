README: Synthetic Dataset Generation of Customer Reviews
1. Introduction
This report presents the methodology implemented for generating a synthetic dataset of customer reviews within the “Supplements/Vitamins” category. The primary objective was to create realistic synthetic data that accurately mimics human-written reviews while incorporating controlled variations in aspects such as length, sentiment, and topic diversity.

2. Methodology
2.1 Data Preparation
2.1.1 Dataset Acquisition
Two primary datasets were utilized in this project:

Product Information Dataset: This dataset (product_asin.csv) contains details about various supplements, including titles and categories.
Customer Reviews Dataset: This dataset (reviews_supplements.csv) comprises reviews submitted by customers regarding the supplements.
These datasets were critical in ensuring that the generated reviews would be contextually relevant and aligned with real user experiences.

2.1.2 Data Cleaning
Data cleaning was performed to enhance the quality and usability of the datasets. The following steps were undertaken:

Handling Missing Values:
In the reviews_supplements.csv dataset, rows containing missing values in the 'title' or 'text' columns were removed to maintain data integrity. After cleaning, the Review Dataset revealed zero missing values across all columns:

mathematica
Copy code
Missing Values After Cleaning in reviews_supplements.csv Dataset:
rating               0
title                0
text                 0
asin                 0
parent_asin          0
user_id              0
timestamp            0
helpful_vote         0
verified_purchase    0
date                 0
time                 0
In the product_asin.csv dataset, missing values in categorical columns (such as 'cat2', 'cat3', etc.) were imputed using the mode to prevent data loss. Following imputation, the product dataset also showed zero missing values:

mathematica
Copy code
Missing Values After Imputation in product_asin.csv Dataset:
X              0
title          0
parent_asin    0
categories     0
cat1           0
cat2           0
cat3           0
cat4           0
cat5           0
cat6           0
2.1.3 Merging Datasets
The two datasets were merged based on a common key ('parent_asin'), resulting in a comprehensive dataset that linked customer feedback with specific products. This merge facilitated the generation of synthetic reviews that accurately reflect the attributes of the products. The merged dataset was subsequently saved as merged_supplements_reviews.csv.

2.2 Model Selection and Template Design
2.2.1 Model Selection
The BART (Bidirectional and Auto-Regressive Transformers) model was chosen for generating synthetic reviews. BART’s architecture combines the strengths of both bidirectional context understanding (similar to BERT) and autoregressive text generation (akin to GPT).

Model Architecture Overview:

Encoder-Decoder Architecture: BART uses a standard encoder-decoder structure, where the encoder processes the input sequence and the decoder generates the output sequence.
Bidirectional Context: The encoder employs bidirectional context, allowing it to understand the entire input sequence before generating an output, which is particularly beneficial for tasks requiring contextual awareness.
Auto-regressive Generation: The decoder generates text in an autoregressive manner, predicting the next word based on previously generated words, leading to coherent and contextually relevant output.
This architecture makes BART well-suited for tasks such as text summarization, translation, and generative tasks like synthetic review generation.

2.2.2 Template Design
To ensure diversity in the generated content, a series of templates for positive, negative, and neutral reviews were established. Each sentiment category included both short and long templates. This structured approach allowed for systematic generation of varied reviews while maintaining realism.

3. Review Generation Process
The model was configured to generate synthetic reviews for each unique product title in the dataset. The generation process involved:

Selecting a template based on the sentiment category.
Randomly determining the length of the review (short or long).
Feeding the selected template to the BART model to produce a synthetic review.
4. Challenges Faced
4.1 Resource Limitations
Significant memory usage was observed during the execution of the review generation process. The execution consumed up to 12.7 GB of RAM, leading to performance issues. Consequently, the runtime had to be terminated and restarted multiple times to manage resources effectively.

4.2 Delimiter Issues
A delimiter problem was encountered while handling CSV files, which affected the ability to read and write data properly. This necessitated a thorough review of the data import/export process to ensure that the generated reviews were saved correctly without data loss.

4.3 Model Limitations
Initially, the BART model did not produce the expected quality of reviews. To address this limitation, pre-defined templates were employed, which guided the model towards generating more relevant outputs. This iterative refinement significantly improved the quality of the generated reviews.

5. Evaluation of Generated Data
5.1 Descriptive Statistics
Average Review Length: The average length of the generated synthetic reviews was 124.21 characters.
Median Review Length: The median length was 114.00 characters.
Sentiment Distribution: The distribution of sentiments among the synthetic reviews was as follows:
Positive: 453
Negative: 453
Neutral: 452
This distribution suggests a balanced representation of sentiments, reflecting the varied nature of actual customer feedback.

5.2 Readability Metrics
Average Flesch Reading Ease: The average score was 60.90, indicating that the reviews are relatively easy to read, suggesting accessibility for a broader audience.
Average Flesch-Kincaid Grade Level: The average grade level was 7.56, indicating that the language used in the reviews is appropriate for 7th-grade readers, making it accessible to a wide demographic.
5.3 Unique Review Count
The total number of unique synthetic reviews generated was 1358. This count reflects the diversity of the output and the effectiveness of the template and model in producing varied content.

6. Insights and Learnings
The implementation highlighted the importance of rigorous data cleaning and preprocessing steps to ensure high-quality inputs for model training. Additionally, the iterative process of refining the model’s output through templates proved to be a valuable learning experience, demonstrating how structured approaches can enhance generative tasks. Furthermore, resource management emerged as a crucial aspect, emphasizing the need for optimization when working with large datasets and complex models.
