 Inspection Process (manual) of issues in [Apache Cassandra](https://github.com/apache/cassandra)

**1. Goal**

The objective of the process is to develop a systematic way to classify issues in the Apache Cassandra Jira Issue Tracker based on their architectural impact. This will help to ensure that issues with the most significant architectural impact are prioritized for resolution.

Input:

The input to the process is a [list of issues selected](https://github.com/Technical-Debt-Large-Scale/my_validation/blob/main/cassandra/my_issues_to_inspection_cassandra.zip) from the Apache Cassandra repository. 

Processing:

The processing of the issues is done manually by a human analyst. The analyst will review the fields of each issue in search of evidence of architectural impact. This evidence can include things like the affected code, the affected components, or the potential impact on the overall architecture.

Output:

The output of the process is a spreadsheet that indicates whether each issue has (yes) or does not have (no) architectural impact. This spreadsheet can be used to prioritize issues for resolution and to track the progress of the issue resolution process.

**2. Key Concepts**

This section highlights the key concepts that should be used as a reference to analyze whether an issue indicates architectural impact.

2\.1 Architectural Impact

Architectural impact refers to problems that affect the software structure, organizational issues, software quality, and the ability to evolve and maintain. This can include:

- Changes to core components
- Performance and scalability improvements
- Resource management
- Changes to the data model
- Distributed system aspects
- Security and compliance, among others.

Using the Apache Cassandra project as a basis, below is the definition and example of each of the architectural impact indicators:

- Changes to core components: Refers to significant changes to the main modules, classes, or structures of the system. This can include rewriting of core modules, replacing key libraries, or changes to the system's main architecture.

Example in Apache Cassandra: An update that replaces the main data storage system with a different technology (for example, from a file-based model to a column-based model).

- Performance and scalability improvements: Includes changes that aim to increase efficiency and the ability to handle a larger volume of data or workload.

Example in Apache Cassandra: Optimization of the read/write algorithm to reduce query response time or implementation of a new partitioning mechanism to improve the horizontal scalability of the database.

- Resource management: Refers to the control and efficient use of resources such as memory, CPU, and storage.

Example in Apache Cassandra: Implementation of a new memory management mechanism to reduce system overhead or adjustments to cache usage to optimize memory utilization.

- Changes to the data model: Changes to the structure, organization, or representation of the data stored.

Example in Apache Cassandra: Adding a new supported data type, changes to the table schema, or optimization of the data structure to improve query efficiency.

- Distributed system aspects: Refers to changes that impact the distribution, communication, or coordination between different parts of the distributed system.

Example in Apache Cassandra: Implementation of a new communication protocol between nodes to improve consistency or introduction of more efficient load balancing strategies.

- Security and compliance: Includes changes related to the system's security, ensuring compliance with regulations, policies, or security best practices.

Example in Apache Cassandra: Implementation of encryption to protect data at rest or in transit, introduction of new access controls to ensure compliance with specific security standards.

These examples illustrate how each of these architectural impact indicators can manifest itself in the context of the Apache Cassandra project, affecting its structure, performance, security, and ability to evolve.

2\.2 Fields Analyzed in Each Issue

The following fields should be analyzed:

- Summary (issue summary)
- Description (issue description)
- Comments (comments) - Contains comments from devs and other stakeholders involved in the issue

These fields should be examined to detect (yes/no) indications of architectural impact.

The summary should be reviewed for any indication that the issue may impact the architecture of the system. The description should be reviewed in more detail for specific information about the issue. The comments should be reviewed for any additional information that may be relevant to the architectural impact of the issue.

The analyst should use their judgment to determine whether the evidence in the issue indicates that it has architectural impact. If the analyst is unsure, they should err on the side of caution and classify the issue as having architectural impact.

**3. Issue Selection for Inspection**

This section shows the selection criteria for issues for inspection (selected issues)

3\.1 Critical Classes

Critical classes are identified by the [ATDCodeAnalyzer](https://github.com/Technical-Debt-Large-Scale/atdcodeanalyzer) (method developed to identify classes affected by ATD). These classes have:

- Architectural Technical Debt (ATD)
- Architectural Smells such as Cycle Dependence or Hub-like Dependence
- High cyclomatic complexity
- High commit frequency
- Cause significant impact (changes) in other parts of the software

Architectural Technical Debt (ATD): Refers to problems or deficiencies in the software architecture that require correction to ensure stability, maintainability, or long-term performance.

Example: In Apache Cassandra, the lack of normalization in storage data, leading to an uneven distribution among nodes, can result in performance and scalability problems. Solving this would require refactoring the storage structure to improve data distribution.

Architectural Smells such as Cycle Dependence or Hub-like Dependence: Are code patterns or architectural structures that indicate potential problems in the architecture, such as cyclic dependencies or excessive concentration of functionality in a single component.

Example: In Apache Cassandra, a cycle dependence between major system modules can make it difficult to modify or expand these modules without affecting others, leading to maintenance problems. Identifying and breaking these cyclic dependencies would be a measure to solve this Architectural Smell.

High cyclomatic complexity: Refers to sections of code with many different execution paths, increasing the difficulty of understanding, testing, and maintaining the code.

Example: In an Apache Cassandra component, a function with a high cyclomatic complexity value may contain multiple nested loops and complex conditional structures, making it difficult to understand and modify without introducing errors. Example of treemap/heatmap of cyclomatic complexity of Apache Cassandra in this link.

High commit frequency: Refers to the rate of changes submitted to the version control repository. A high commit frequency can indicate a high level of activity and constant changes in a particular part of the code.

Example: If a specific area of Apache Cassandra receives frequent commits for bug fixes or improvements, this may indicate a problematic area or a constant demand for changes, suggesting the presence of architectural problems or refactoring needs. Example of treemap/heatmap of file commit frequency in Apache Cassandra in this link.

Cause significant impact (changes) in other parts of the software: Refers to changes in a component that have a cascading effect in other areas of the system, requiring modifications in multiple locations to maintain global integrity or functionality.

Example: A change in the Apache Cassandra data structure that affects the data access logic may require changes in different parts of the system, such as in the read/write methods or in the data abstraction layers, thus impacting most of the system's functionalities.

**4. Detailed Process for Issue Analysis**

4\.1 Present the Fundamental Concepts

The issue inspector must understand the basic concepts to apply them in the inspections.

In Step 1 (Introduction), the focus is on understanding the concepts of:

- Software Architecture
- Architectural Impact
- Technical Debt (TD)
- Architectural Technical Debt (ATD)
- Self-Admitted Technical Debt (SATD)
- Commits
- Issues

Software Architecture: Software architecture refers to the fundamental structure of a software system. It encompasses the high-level decisions about the organization of components, the communication between them, the patterns used, and the system's constraints. This structure defines how the software is built, making it easier to understand, maintain, and evolve the system over time.

Architectural Impact: Architectural impact is the consequences of changes or decisions in the architecture of a software. It refers to changes that affect the structure, performance, security, scalability, or any other fundamental characteristic of the system. These impacts can be positive, such as improvements in efficiency, or negative, such as the introduction of performance problems.

Technical Debt (TD): Technical debt is a metaphor that describes technical commitments made during software development. It refers to decisions that prioritize quick delivery over quality, leading to areas of code that need refactoring, improvements, or fixes in the future. It is a concept that highlights the long-term cost of quick and not-ideal choices made during development.

Architectural Technical Debt (ATD): Architectural technical debt is a type of technical debt that is specifically related to software architecture. It involves commitments or decisions that impact the fundamental structure of the system, such as inadequate design patterns, excessive dependencies between modules, or lack of modularity.

Self-Admitted Technical Debt (SATD): Self-admitted technical debt, or SATD (Self-Admitted Technical Debt), refers to technical debts that the developers themselves recognize and explicitly document in the code, in comments, or in commit logs. This helps to identify problematic areas that need future attention.

Commits: are the basic units of change in the version control of a system. A commit represents a specific change made by a developer and includes information about which files were modified, the lines of code changed, and a message that describes the change.

Issues: are units of work in the context of software project management. They can represent tasks, bugs, improvements, or any other activity to be performed. They are generally recorded in issue tracking systems (such as Jira), containing information about the nature of the problem, its priority, owners, and status.

4\.2 Show Examples of Issues

In Step 2 (Exhibition of Examples), samples of issues are presented:

- Examples of issues with architectural impact (5 issues with architectural impact)
- Examples of issues without architectural impact (5 issues without architectural impact)

4\.3 Use of SATD Keywords

We implemented a method to extract SATD keywords from commit messages and code comments. We used academic references to identify 235 SATD keywords.

The following 235 keywords were used to identify potential TD in issues (summary, description and comments) and commits (messages and diffs):

keywords = ['API', 'FIXME', 'TODO', 'ability to evolve', 'ability to handle increased load', 'annotation', 'anti-pattern', 'any chance of a test', 'architectural debt', 'architectural issue', 'architectural problem', 'architectural smell', 'avoid calling it twice', 'avoid extra seek', 'bad practice', 'brittle code', 'buggy code', 'by hard coding instead of', 'cast', 'checkstyle errors', 'circular dependency', 'clean', 'clean up code', 'cleanup', 'code cleanup', 'code complexity', 'code debt', 'code defect', 'code dependencies', 'code difficulty', 'code duplication', 'code entanglement', 'code flaw', 'code improvement', 'code interdependencies', 'code issue', 'code problem', 'code redundancy', 'code restructuring', 'code rot', 'code simplification', 'code smell', 'cognitive complexity', 'comment', 'complex code', 'complex code relationships', 'complexity', 'concrete code', 'concurrency issue', 'confusing', 'constructor', 'cross-module', 'cyclic dependency', 'cyclomatic complexity', 'dead code', 'debug', 'delicate code', 'dependability', 'dependencies', 'dependency', 'deprecated code', 'design', 'design debt', 'design defect', 'design flaw', 'design flaws', 'design issue', 'design problem', 'design smell', 'difficult to maintain code', 'difficult to understand code', 'disorganized code', 'documentation', 'documentation debt', 'documentation does not mention', "documentation doesn't match", 'duplication', 'ease of maintenance', 'easy to break code', 'encapsulation', 'endpoints', 'error message', 'exception', 'exposed internal state', 'extension point', 'fault tolerance', 'files', 'findbugs', 'fix', 'flaky', 'flaky code', 'formatting', 'fragile code', 'get rid of', 'good to have coverage', 'hack', 'handling', 'hard-coded strings', 'hard-coded values', 'header', 'implementation', 'implementation debt', 'improvement', 'inconsistency', 'indirect dependency', 'ineffective solution', 'ineffective way', 'inefficient solution', 'inefficient way', 'infinite loop', 'inter-module', 'interface', "it'd be nice", "it's not perfectly documented", 'javadoc', 'lack of abstraction', 'lack of code comments', 'lack of cohesion', 'lack of documentation', 'lack of encapsulation', 'lack of generalization', 'lack of information hiding', 'lack of modularity', 'lack of separation of concerns', 'lack of test cases', 'lack of testing', 'latency', 'lead to huge memory allocation', 'leak', 'less verbose', 'literal strings', 'literal values', 'logging', 'magic numbers', 'magic strings', 'maintainability', 'maintainability issue', 'make it less brittle', 'makes it much easier', 'makes it very hard', 'minor', 'misleading', 'modularity', 'module dependencies', 'module-to-module', 'monolithic code', 'more efficient', 'more readable', 'more robust', 'more tests', 'more tightly coupled than ideal', 'multithreading issue', 'naming', 'need to update documentation', 'no longer needed', 'not done yet', 'not implemented', 'not supported yet', 'not thread safe', 'not used', 'output', "patch doesn't apply cleanly", 'performance', 'please add a test', 'poor solution', 'poor way', 'poorly documented code', 'poorly structured code', 'poorly tested code', 'quick fix', 'race condition', 'reduce duplicate code', 'redundant', 'refact', 'refactor', 'refactoring', 'reliability', 'rename', 'repeated code', 'response time', 'robustness', 'scalability', 'scalability issue', 'short term solution', 'should be updated to reflect', 'should improve a bit by', 'simplify', "solution won't be really satisfactory", 'some holes in the doc', 'spaghetti code', 'speed', 'speed up', 'spurious error messages', 'suboptimal solution', 'suboptimal way', 'support for', 'synchronization issue', 'system dependencies', 'system design problem', 'takes a long time', 'technical debt', 'technical debt due to architectural issues', 'technical debt due to design issues', 'technical kludge', 'temporary solution', 'test', "test doesn't add much value", 'testing debt', 'there is no unit test', 'throughput', 'tidy up', 'tight coupling', 'too long', 'too much', 'trustworthiness', 'typo', 'ugly', 'undocumented code', 'undocumented strings', 'undocumented values', 'unnecessary', 'unreliable code', 'unstable', 'untested code', 'unused', 'unused code', 'unused import', 'update', 'violation', 'wastes a lot of space', 'work in progress', 'workaround', 'would significantly improve', 'wrong solution', 'wrong way']

Categories of SATD keywords

The SATD keywords were categorized into the following categories:

- Design: These keywords indicate problems with the design of the software, such as "spaghetti code", "god object", or "fragile architecture".
- Implementation: These keywords indicate problems with the implementation of the software, such as "duplicate code", "hard-coded values", or "inefficient algorithms".
- Testing: These keywords indicate problems with the testing of the software, such as "no unit tests", "incomplete test coverage", or "flaky tests".
- Documentation: These keywords indicate problems with the documentation of the software, such as "missing documentation", "outdated documentation", or "incorrect documentation".
- Other: These keywords indicate other problems with the software, such as "performance problems", "security vulnerabilities", or "scalability issues".

Examples of SATD keywords

Here are some examples of SATD keywords:

- Design:
  - "spaghetti code"
  - "god object"
  - "fragile architecture"
  - "tight coupling"
  - "high coupling"
  - "low cohesion"
- Implementation:
  - "duplicate code"
  - "hard-coded values"
  - "inefficient algorithms"
  - "null pointer dereferences"
  - "resource leaks"
  - "memory leaks"
- Testing:
  - "no unit tests"
  - "incomplete test coverage"
  - "flaky tests"
  - "regressions"
  - "test debt"
- Documentation:
  - "missing documentation"
  - "outdated documentation"
  - "incorrect documentation"
  - "incomplete documentation"
  - "hard-to-understand documentation"
- Other:
  - "performance problems"
  - "security vulnerabilities"
  - "scalability issues"
  - "maintainability problems"
  - "extensibility problems"

The use of SATD keywords can be a useful tool for identifying potential TD in software systems. By identifying these problems early on, developers can take steps to address them and avoid costly downstream problems.

4\.4 List of Issues for Inspection

This section provides a link to the list of issues that were selected for manual inspection. This list includes issues that were identified using the SATD keywords and the other criteria described in the previous sections.

Available at[ ](https://github.com/Technical-Debt-Large-Scale/my_validation/blob/main/cassandra/my_issues_to_inspection_cassandra.zip)<https://github.com/Technical-Debt-Large-Scale/my_validation/blob/main/cassandra/my_issues_to_inspection_cassandra.zip>

These issues were selected for manual inspection (to indicate whether the issue has or does not have architectural impact)

**5. Classification of Issues**

This section describes the process for classifying each issue as having or not having architectural impact. The inspector will review the issue and use their judgment to determine whether the issue has the potential to impact the architecture of the system. If the inspector believes that the issue has architectural impact, they will label the issue as "Yes". Otherwise, they will label the issue as "No".

Each issue is labeled as 'Yes' (indicating architectural impact) or 'No' (no architectural impact) after analysis.

Original document: https://docs.google.com/document/d/1umbEJMVsdxTzBVOr8VDRCscpwOK9-ePVJ-o862L5j08
