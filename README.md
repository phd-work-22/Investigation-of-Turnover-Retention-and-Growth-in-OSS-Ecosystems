# Investigation of Turnover Retention and Growth in OSS Ecosystems

The steps of conducting our work refer to the previous work in Tulili et al. (2025). The details of the methodology can be accessed through the link:

1. **Data collection** -- This study used two primary datasets to examine the dynamics of developer sentiment and activity within the Gentoo, Apache, and GCC open-source ecosystem. These datasets include:

_Mailing list archive (January 2001–December 2024): _
Technical discussions and communications were extracted from Gentoo’s, Apache's, and GCC's official archive website. 
Each entry was annotated with metadata such as the timestamp, sender, recipient and subject line. This dataset was extracted, cleaned and prepared using automated scripts, forming the basis for sentiment analysis that examined developer interactions across different phases of the project.

As the output of the source code are formed into many files, we integrated all files into one file for each community with the R.
We put the mailing list data into the database (the source code used was insert_gentoo_mlists_to_masterTable-forReplication.py
Commit history dataset (July 2000–December 2024): Commit logs were retrieved directly from Gentoo's GitHub repository using the \textit{git clone} command. 
The dataset was structured into a database. 
Each commit was annotated with key metadata, including committer details (e.g., name and email), timestamps, commit hashes and file paths. These details enabled precise mapping of developer activities to specific categories within the Gentoo ecosystem. 

2. **Data Preprocessing **
2.1 Mailing list preprocessing 
The body content of each email was divided into individual sentences. To remove noise and irrelevant information, we applied the following cleaning steps:

Removed sentences prefixed by the character ‘\textgreater’, which typically denote quoted replies.
Stripped URLs, names or signatures and greeting phrases (e.g., “Kind Regards” and “Best Regards”).
Eliminated sentences containing code syntax, HTML, or XML tags. The source code used was NormalisedGentooMListsReport.java. The output of this file wasgentoo_mlists_normalised_komen.txt.
This process resulted in a clean dataset of sentences, each assigned a sentiment score using the SentiStrength-SE tool.

Source code for sentiment labeling: ExecuteSentistrengthSE.java; output: results of sentimen analysis gentoo mlists.txt. File included is sentistrength.sh. In order to giving the scores to each sentence, we have to compile and run the ExecuteSentistrengthSE.java together with file '<oss_name>_mlists_normalised_komen.txt' as its input and its ouput as 'results of sentimen analysis <oss_name> mlists.txt'. The 'results of sentimen analysis <oss_name> mlists.txt' was put into a table in the database and the code used was InsertingResults.java

3.** Data Analysis**
The analysis phase of this study involved data aggregation and statistical techniques to investigate the relationship between developer sentiment and activity within the Gentoo ecosystem. Specifically, we analyzed both negative and positive sentiments expressed in mailing list communications and their associated activity levels in the commit dataset.

3.1 Linking and aggregating sentiment data To address RQ1, we integrated sentiment data with commit activity by aligning records based on timestamps (year, month, day). This integration allowed us to aggregate the number of positive and negative messages for each file path annually. To evaluate sentiment trends over time, we calculated the net sentiment difference (positive minus negative messages) and normalized the results using z-score normalization. Categories were ranked from most negative to most positive and the results were visualized in a heatmap and in a table (provided in the appendices).

3.2.Sampling categories for analysis 
We selected a representative 15% sample, resulting in 40, 6, and 6 categories for Gentoo, Apache, and GCC respecively for further analysis. These included the twenty most negative and the twenty most positive categories of Gentoo based on sentiment scores; and three most negative and three most positive categories of Apache and GCC based on sentiment scores. 

This approach ensured a balanced investigation of extremes in sentiment-affected components while maintaining analytical feasibility.

The code used was hmaps-sentiment-standardnorm.R

Calculating workforce dynamics We analyzed three key workforce dynamics—retention, turnover and growth rates—within the sampled categories. The codes used were analysing RR TR GR monthly-for replication.R and calculating matrix corr-for replication.R

Please see our paper for more details of the workforce dynamics. All the dataset are available by request.
