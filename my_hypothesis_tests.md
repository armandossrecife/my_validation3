# My Hypothesis tests

To verify the hypotheses we can use the following approach:
## 1. Identify the null and alternative hypotheses.

The null hypothesis is the statement that the three characteristics listed are not associated with issues with architectural impact. 

The alternative hypothesis is the statement that the three characteristics are associated with issues with architectural impact.

## 2. The statistical test (Chi-squared test, Mann-Whitney U test). 

The choice of statistical test will depend on the specific characteristic you are testing. 
For example, to test the hypothesis that issues with architectural impact affect a substantial number of files, you can use a chi-squared test. 
To test the hypothesis that issues with architectural impact issues with architectural impact require more time for resolution you can use a Mann-Whitney U test.

## 3. Collect data. 

We will need to collect data on the **number of files** affected, the **number of lines of code changed**, and the **time to resolution** for both issues with architectural impact and issues with less architectural impact.

## 4. Calculate the test statistic and p-value. 

The test statistic is a measure of the evidence against the null hypothesis. 

The *p-value* is the probability of obtaining a test statistic as extreme or more extreme than the one you observed, assuming that the null hypothesis is true.

## 5. Make a decision. 

If the *p-value* is less than your chosen significance level, then you reject the null hypothesis and conclude that the evidence supports the alternative hypothesis.

# T1: HA - issues with architectural impact involve significant code changes

To test the hypothesis that issues with architectural impact involve significant code changes:

**Null hypothesis (H0A)**: The number of lines of code changed by issues with architectural impact is not significantly different from the number of lines of code changed by issues with less architectural impact.

**Alternative hypothesis (H1A)**: The number of lines of code changed by issues with architectural impact is significantly greater than the number of lines of code changed by issues with less architectural impact.

**Statistical test**: Mann-Whitney U test

| T1:HA   	| Cassandra | ActiveMQ | Kafka	   |
| --------- | --------- | -------- | --------- |
| p-value 	| 0.00108   | 0.01891  | 0.00022   |
| H0A 		| Rejected  | Rejected | Rejected  |
| H1A 		| Accepted  | Accepted | Accepted  |


# T2: HA - issues with architectural impact affect a substantial number of files

To test the hypothesis that issues with architectural impact affect a substantial number of files:

**Null hypothesis (H0A)**: The number of files affected by issues with architectural impact is not significantly different from the number of files affected by issues with less architectural impact.

**Alternative hypothesis ((H1A)**: The number of files affected by issues with architectural impact is significantly greater than the number of files affected by issues with less architectural impact.

**Statistical test**: Mann-Whitney U test

# T3: HC - issues with architectural impact require more time for resolution

To test the hypothesis that issues with architectural impact require more time for resolution:

**Null hypothesis (HC0)**: The time to resolution for issues with architectural impact is not significantly different from the time to resolution for issues with less architectural impact.

**Alternative hypothesis (HC1)**: The time to resolution for issues with architectural impact is significantly greater than the time to resolution for issues with less architectural impact.

**Statistical test**: Mann-Whitney U test
