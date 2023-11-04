# Analysis Method

Analysis of commits and issues from Git Repositories

## Apache Cassandra analysis

Draft of Cassandra's commit and issue analysis method

![My analysis of commits and issues from Cassanddra](https://raw.githubusercontent.com/armandossrecife/my_validation3/main/imagens/my_method_analysis_commits_issues.jpg)

1. Filtering (A) - Cassandra Project:
This step involves selecting and filtering data related to the Apache Cassandra project from the GitHub repository. 

2. Filtering (A) - Commits with Critical Classes:
After filtering the Cassandra project data, you further narrow down the focus by identifying commits that involve critical classes. Critical classes may be those that are related to architectural or high-impact changes.

3. Filtering (B) - Cassandra Project:
In this step, you do a similar filtering process but on the Jira Issue Tracker, specifically looking for issues related to the Cassandra project.

4. Filtering (B) - Issues with Commits with Critical Classes:
This step involves identifying Jira issues that are associated with commits containing critical classes. It's a way to link code changes with corresponding issues.

5. Random Sample Selection from 4 that results in 226 issues:
Here, you randomly select a subset of the filtered issues. The reason  is for further analysis.

6. Manual classification of issues to check architectural impact:
You manually review and classify the selected 226 issues to assess their architectural impact. This could involve identifying whether the issue relates to architectural changes, refactoring, or other factors.

7. Semi-automatic classification aided by ChatGPT with Prompt Engineering:
In this step, you use ChatGPT to assist in the classification process. You might provide prompts to ChatGPT to help automate or semi-automate some of the classification tasks. More details in https://github.com/armandossrecife/my_validation3/blob/main/inspection_process.md

8. Degree of Agreement Calculation comparing 6 and 7:
This step involves calculating the degree of agreement between the manual classification and the semi-automatic classification performed with the help of ChatGPT. You need to quantify how closely the two methods align.

9. Degree Agreement using Cohen's Kappa:
Cohen's Kappa is a statistical measure used to assess the agreement between two raters (in this case, the manual and ChatGPT-assisted classifications). It takes into account the possibility of agreement occurring by chance.

The calculated Cohen's Kappa score was found to be 0.752, indicating a substantial level of agreement between manual inspection and ChatGPT inspection.

In our evaluation of the model used for inspecting issues, we obtained the following key performance metrics: Precision: 0.667, Recall: 1.00, Accuracy: 0.92 and F1-Score: 0.8. 

More details and scripts available in https://github.com/armandossrecife/my_validation3/blob/main/my_analysis_cassandra.ipynb

## Apache ActiveMQ analaysis

ActiveMQ analysis

![My analysis of commits and issues from ActiveMQ](https://github.com/armandossrecife/my_validation3/blob/main/imagens/my_method_analysis_commits_issues_activemq.jpg)

More details and scripts available in https://github.com/armandossrecife/my_validation3/blob/main/my_analysis_activemq.ipynb

## Apache Kafka analysis

Kafka analysis

![My analysis of commits and issues from Kafka](https://github.com/armandossrecife/my_validation3/blob/main/imagens/my_method_analysis_commits_issues_kafka.jpg)

More details and scripts available in https://github.com/armandossrecife/my_validation3/blob/main/my_analysis_kafka.ipynb

# Comparing Results

The comparison among Cassandra, Kafka and ActiveMQ is available in

https://github.com/armandossrecife/my_validation3/blob/main/my_comparison.ipynb
