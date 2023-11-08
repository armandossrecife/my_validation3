# Analysing Issues with Architectural Impact

Analysis of commits and issues from Git Repositories using Critical Classes from [ATDCodeAnalyzer](https://github.com/mining-software-repositories/cassandra/blob/main/data/AnalysisCassandraRepositoryFlow.png).

We have been analysed three Git Repositories: Apache Cassandra, Apache ActiveMQ and Apache Kafka. 

## Apache Cassandra analysis

Draft of Cassandra's commit and issue analysis method

![My analysis of commits and issues from Cassanddra](https://raw.githubusercontent.com/armandossrecife/my_validation3/main/imagens/my_method_analysis_commits_issues.jpg)

1. Filtering (A) - Cassandra Project:
This step involves selecting and filtering data related to the Apache Cassandra project from the GitHub repository.

3. Filtering (A) - Commits with Critical Classes:
After filtering the Cassandra project data, you further narrow down the focus by identifying commits that involve critical classes. Critical classes may be those that are related to architectural or high-impact changes.

4. Filtering (B) - Cassandra Project:
In this step, you do a similar filtering process but on the Jira Issue Tracker, specifically looking for issues related to the Cassandra project.

5. Filtering (B) - Issues with Commits with Critical Classes:
This step involves identifying Jira issues that are associated with commits containing critical classes. It's a way to link code changes with corresponding issues.

6. Random Sample Selection from 4 that results in 226 issues:
Here, you randomly select a subset of the filtered issues. The reason  is for further analysis.
Based on a normal continuous random variable from [ScyPY](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.norm.html)
Based on the parameters: confidence_level = 0.95, margin_of_error = 0.05, population_proportion = 0.8 and population_size = len(issues_with_commits_with_critical_classes)
sample_size = calculate_sample_size(confidence_level, margin_of_error, population_proportion, population_size)
norm.ppf(): normal continuous random variable

7. Manual classification of issues to check architectural impact:
You manually review and classify the selected 226 issues to assess their architectural impact. This could involve identifying whether the issue relates to architectural changes, refactoring, or other factors.

8. Semi-automatic classification aided by ChatGPT with Prompt Engineering:
In this step, you use ChatGPT to assist in the classification process. You might provide prompts to ChatGPT to help automate or semi-automate some of the classification tasks. More details in https://github.com/armandossrecife/my_validation3/blob/main/inspection_process.md

9. Degree of Agreement Calculation comparing 6 and 7:
This step involves calculating the degree of agreement between the manual classification and the semi-automatic classification performed with the help of ChatGPT. You need to quantify how closely the two methods align.

10. Degree Agreement using Cohen's Kappa:
Cohen's Kappa is a statistical measure used to assess the agreement between two raters (in this case, the manual and ChatGPT-assisted classifications). It takes into account the possibility of agreement occurring by chance.

The calculated Cohen's Kappa score was found to be 0.752, indicating a substantial level of agreement between manual inspection and ChatGPT inspection.

In our evaluation of the model used for inspecting issues, we obtained the following key performance metrics: Precision: 0.667, Recall: 1.00, Accuracy: 0.92 and F1-Score: 0.8. 

This semi-automatic inspection process (aided by ChatGPT) can help to inspect other issues from other apache projects. 

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

The comparison among Cassandra, ActiveMQ and Kafka

![Boxplot Lines - LOC - changes in Commits in issues with AI](https://github.com/armandossrecife/my_validation3/blob/main/imagens/boxplot_lines_chagnes_in_commits_issues_with_ai.png)
![Boxplot Files chagnes in Commits in issues with AI](https://github.com/armandossrecife/my_validation3/blob/main/imagens/boxplot_files_chages_in_commits_issues_with_ai.png)
![Boxplot Issues Time Resolution](https://github.com/armandossrecife/my_validation3/blob/main/imagens/boxplot_timeresolution_issues.png)

**Conclusions**
Issues with architectural impact (labeled as "Yes") exhibit the following **characteristics**:
- They affect a substantial number of files (as indicated by the 2rd end 3rd quartile of files modified in the commit).
- They involve significant code changes (as demonstrated by the 2rd end 3rd quartile of lines modified in the commit).
- They require more time for resolution (as evidenced by the 2rd end 3rd quartile of the time taken to resolve issues with architectural impact).

**Justification**
These conclusions are drawn from a comparative analysis of results from the Cassandra, ActiveMQ, and Kafka repositories, specifically:
- A comparison of the results related to the number of lines and files modified in issue commits with architectural impact (labeled as "Yes").
- A comparison of the results concerning the average time required to resolve issues with architectural impact (also labeled as "Yes").

Furthermore, the inspection of issues that appear in commits containing critical files and have an architectural impact underscores the influence of critical classes on software architecture.

**Contributions**

- We created an LLM model, based on prompt engineering, to help identify issues with architectural impact.
- We provided a dataset (Apache Cassandra, Apache ActiveMQ and Apache Kafka) of commits, issues that have architectural impact
- We provided a dataset (Apache Cassandra, Apache ActiveMQ and Apache Kafka) of text with details about inspections of issues with architectural impact and issues without architectural impact

More details in 

https://github.com/armandossrecife/my_validation3/blob/main/my_comparison.ipynb
