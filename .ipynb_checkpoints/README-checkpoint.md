
# Sentiment comparison analysis between user discussions and Corona mask requirement Articles clustered into subject areas (Code)

The Der Standard database's raw text data is utilized and modified by this repository to cluster articles into groups and examine the temporal shift in sentiment of user comments for each article group.

#### Directory Structure

- comments: pipeline for user comment data (article pipeline should be done first)
- comparison: sentiment comparison analyze code after both pipeline were successful
- content: pipeline for article data
- data: contains all the stored data .csv that are needed for further processing and analysation.

To run all the notebooks successful follow this guide step by step

### Corona Article Content Pipeline (in directory /content)

1. To preprocess the data and obtain the preprocessed content, run the "preprocessing.ipynb" file. The input data is the raw export data from the Database, which may not be included in the data directory of this repository.
2. To cluster similar articles, go to the /clustering directory and run the "KMean-clustering.ipynb" file. The input is the preprocessed data frame, and the output is a set of CSV files in the ../data/feature directory. Each CSV file corresponds to a cluster found, and there is also an "knn_clustering.csv" file that shows the cluster value for each article.
3. To perform opinion mining and see the most important phrases and words per cluster, go to the /opinion directory and run the "TFIDS-Cluster.ipynb" file. First, manually label each cluster with the help of the TFIDS scores. Then, input the CSV files for each cluster that were calculated before and stored under ../data/feature/cluster. The output is a CSV file "tfids_cluster.csv" that shows the important phrases per cluster in a single table. In the last cell, you can find the cluster description in commented lines.
4. To compare the supervised clusters given by Der Standard with our clusters, run the "DerStandard_Classifier.ipynb" file. The output is two CSV files: "supervise_clustered_content.csv", which contains the keywords for each of our found clusters, and "supervise_classified_content.csv", which contains keywords per article. This step is not necessary for the further text pipeline but may be interesting to see.
5. To calculate the sentiment score for each word in each article for later comparison, run the "Sentiment_Score.ipynb" file. The input is the preprocessed content and the _sentiws_ dictionary. The output is a file "sentiws_content.csv" that contains the calculated scores for each article.

### Corona Postings Pipeline (in directory /comments)

1. To preprocess the raw export data, run the "preprocessing.ipynb" file. Note that the raw data is not included in this repository, and there are over 500k comments, so the preprocessing is done in multiprocess to save time. If the pipeline frequently shuts down, you can use the "mergingBigFrame.ipynb" notebook from a previous attempt to merge smaller preprocessing frames together.
2. To calculate the sentiment score for each comment and the overall sub-discussions, go to the /sentiment directory and run the "sentiment_comment.ipynb" file. The input is the preprocessed data in a .zip file to save space. The output is a CSV file "sentiws_comment.csv" that shows all relevant scores for further analysis.

### Comparison Analysis

3. run "sent_plots.ipynb" in the /comparison folder for comparing the sentiment scores. Input are the feature files for the corona article content (clustering and sentiment scores) and output are different plots and a CSV file (content_interesting.csv) containing interesting articles, where the community sentiment was completely different to the article's one.
4. run "viral-article.ipynb" in the /comparison folder to see the content to comments relations in plots.
