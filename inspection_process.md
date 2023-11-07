# Inspection process aided by ChatGTP

We utilized the ChatGPT tool, implementing Few-shot and Chain-of-thought prompting strategies, to expedite the manual inspection of each issue and identify architectural problems. This decision to employ the tool was aimed at streamlining our inspection process. (https://www.promptingguide.ai/pt)

As a software developer, we created a classifier of issues from the Apache Cassandra issue tracker. The classifier analyzes each issue and determines whether or not it has an architectural impact. The issue labeling process is related to check if the label impacts or no impacts the software architecture of the analyzed repository. 

To enable issue labeling, we followed a structured set of stages to enhance the quality of the labeling process.

In **Stage 1** (Introduction), we focused on gaining a deep understanding of the context of Software Architecture, Architectural impact, Technical Debt (TD), Architectural Technical Debt (ATD), Self-Admitted Technical Debt (SATD), commits, and issues, along with their interconnections.

In **Stage 2** (Example Showcase), we presented several sample issues, provided instructions and examples for identifying 'Architectural Impact,' and introduced the 'Architectural Impact Classifier' and 'Issues with Architectural Technical Debt.' We also offered numerous examples of issues with ATD and issues without ATD.

**Stage 3** (Data Preparation) involved the selection of 163 issues for manual inspection to identify architectural issues and technical debt. These issues were chosen based on their association with commits containing critical classes identified by the ATDCodeAnalyzer and featuring SATD keywords in the commit messages and comments of the commit diffs.

**Stage 4** (Final instruction to start the inspection by ChatGPT)

Following the identification of critical issues, each one underwent a thorough inspection. We analyzed the content within the 'summary,' 'description,' and 'comments' fields to detect the presence of SATD keywords. Issues containing these keywords in these fields then underwent a secondary inspection to evaluate their impact on the software's architecture.

This inspection process unfolded in two distinct phases. In the first phase (Manual Inspection), we manually inspected a sample of 163 critical issues. Each issue was labeled 'yes' or 'no' to signify whether it had an impact on the software's architecture. Subsequently, in the second phase (ChatGPT Inspection), the same 163 selected critical issues underwent automatic inspection with the assistance of ChatGPT, generating similar 'yes' or 'no' results concerning their architectural impact.

At the conclusion of this process (Manual Review), we calculated the Cohen's Kappa coefficient to measure the agreement between the results obtained in the first and second phases. This assessment helped determine the consistency between manual and automatic inspections, thereby contributing to a precise analysis of the relationship between critical issues and their effect on the software's architecture

Is this step we use the following stages to use the ChatGTP: 

# Setup ChatGPT to aid issue inspection (Stage1, Stage2, Stage3 and Stage 4)

The stage 3 is just the manual seleciont of the 163 files to be passed after stage 4 is ready to start the inspection process. 

All the 16 prompts (S1P1..S1P4, S2P1..S2P11 and S4P1) must be executed in this sequence to model be effectively. 

# Stage 1 - Introduction:

We start with an introduction to Architectural Technical Debt (ATD) and Self-admitted Technical Debt (SATD), explaing the concepts, techniques, and types of ATD, providing examples. We discuss different issue types in Jira Cassandra and introduce Apache Cassandra. We also share examples of SATD keywords in commits, including their presence in messages and differences in modified files, as well as in Cassandra issue fields such as summary, description, and comments.

You can see the following prompts: S1P1..S1P4

## Prompt1 (S1P1): 
```bash
# Stage 1 #
## Introduction ##
### Contextualization ### 
Lets talk about the following topics: Software Architecture, Architectural Issues, Technical Debt (TD), Architectural Technical Debt (ATD) and Self-admitted Technical Debt (SATD).
```
## Answer1 (S1A1): 
```bash
Certainly, let's provide an overview of the key concepts related to software architecture, architectural issues, technical debt, architectural technical debt (ATD), and self-admitted technical debt (SATD):

Software Architecture:

Software architecture refers to the high-level structure of a software system. It defines the system's components, their relationships, and the principles and guidelines governing their design. It is a blueprint that provides a foundation for software development and maintenance.
Architectural Issues:

Architectural issues are problems or concerns related to the design and structure of a software system. These issues can arise due to architectural decisions, such as the choice of patterns, components, or communication mechanisms. Resolving architectural issues is crucial for maintaining a healthy and scalable software architecture.
Technical Debt (TD):

Technical debt is a metaphorical concept that describes the trade-off between the short-term benefits of rapid development and the long-term costs of code that is not ideal or maintainable. It represents tasks or issues that need to be addressed in the future to ensure the software remains robust.
Architectural Technical Debt (ATD):

Architectural technical debt (ATD) specifically relates to issues in the software architecture. These issues can include design flaws, outdated components, or architectural choices that need reevaluation. ATD can accumulate over time if architectural concerns are not properly addressed.
Self-admitted Technical Debt (SATD):

Self-admitted technical debt (SATD) refers to technical debt that developers or teams explicitly acknowledge within the codebase. SATD is typically documented in code comments, commit messages, or issue trackers. It can help in identifying and prioritizing areas that require architectural improvement.
Understanding these concepts is essential for managing software systems effectively. Addressing architectural issues and technical debt, including ATD and SATD, is critical for maintaining a software system's health, scalability, and long-term viability. It involves making informed decisions, prioritizing work, and continuously improving the software architecture.
```

## Prompt2 (S1P2): 
```bash
# Stage 1 #
## Introduction ##
### Contextualization ### 
Another important topic that could be usefull and related to architectural issue, ATD, TD and SATD is save Tasks or Issues in Issue Tracker System, because it can keep a history of all tasks about improvement, bug-fix, and new features implemented in the software system. Generally, an issue has important data like issue_id, summary, description and comments that contains a lot of important information about improvement task, bug-fix task or new feature task to help developers to work in the issues.
```

## Answer2 (S1A2): 
```bash
Absolutely, the use of an Issue Tracker System is a crucial component in the context of managing architectural issues, ATD, TD, and SATD. These systems provide a structured and organized way to track and manage tasks and issues related to software development. Here's how the Issue Tracker System relates to the topics you've mentioned:

Issue Tracker System:

An Issue Tracker System, often known as a bug tracking system or project management tool, is a software application used by development teams to log, manage, and track various tasks and issues related to software development projects.
Task Management:

Issue Tracker Systems are used to manage a wide range of tasks, including bug fixes, new feature development, code improvements, and architectural enhancements. Each task is typically assigned a unique issue_id.
Information Storage:

Issues in the tracker system contain important data, including:
Summary: A brief description of the task or issue, which provides a quick overview.
Description: A detailed explanation of the task, often including its scope, objectives, and any relevant background information.
Comments: Ongoing discussions and updates related to the issue, allowing developers to collaborate and document progress.
Architectural Issues and ATD:

Issues related to architectural problems and ATD can be tracked within the system. For example, if there is a known architectural flaw, it can be logged as an issue, including a detailed description and potential solutions. This helps in the structured management and resolution of architectural concerns.
Technical Debt and SATD:

Technical debt, including SATD, can also be documented and tracked within the system. Developers can explicitly mention technical debt in comments or issue descriptions. This makes it easier to prioritize and address technical debt as part of the development process.
Collaboration and Communication:

The comments section within an issue allows for collaborative discussions and communication between team members. This is crucial for addressing and resolving architectural issues, technical debt, and other tasks effectively.
History and Tracking:

Issue Tracker Systems maintain a history of all tasks and their statuses. This history is invaluable for tracking the progress of tasks, understanding the evolution of the software, and making informed decisions about resource allocation and prioritization.

In summary, the Issue Tracker System plays a pivotal role in the software development process by providing a centralized and structured platform for tracking, managing, and resolving various tasks and issues, including architectural concerns, technical debt, and self-admitted technical debt. It is a valuable tool for maintaining and improving the quality of software systems over time.
```

## Prompt3 (S1P3): 
```bash
# Stage 1 #
## Introduction ##
### Keywords Samples ### 
keywords found in the content of message commits, modified files diff in commits, and issue content from the issue tracker. These kinds of SATD keywords show technical debt in the item that the developer registers the keyword. Here are some of examples of SATD keywords:
API
FIXME
TODO
ability to evolve
ability to handle increased load
annotation
anti-pattern
any chance of a test
architectural debt
architectural issue
architectural problem
architectural smell
avoid calling it twice
avoid extra seek
bad practice
brittle code
buggy code
by hard coding instead of
cast
checkstyle errors
circular dependency
clean
clean up code
cleanup
code cleanup
code complexity
code debt
code defect
code dependencies
code difficulty
code duplication
code entanglement
code flaw
code improvement
code interdependencies
code issue
code problem
code redundancy
code restructuring
code rot
code simplification
code smell
cognitive complexity
comment
complex code
complex code relationships
complexity
concrete code
concurrency issue
confusing
constructor
cross-module
cyclic dependency
cyclomatic complexity
dead code
debug
delicate code
dependability
dependencies
dependency
deprecated code
design
design debt
design defect
design flaw
design flaws
design issue
design problem
design smell
difficult to maintain code
difficult to understand code
disorganized code
documentation
documentation debt
documentation does not mention
documentation doesn't match
duplication
ease of maintenance
easy to break code
encapsulation
endpoints
error message
exception
exposed internal state
extension point
fault tolerance
files
findbugs
fix
flaky
flaky code
formatting
fragile code
get rid of
good to have coverage
hack
handling
hard-coded strings
hard-coded values
header
implementation
implementation debt
improvement
inconsistency
indirect dependency
ineffective solution
ineffective way
inefficient solution
inefficient way
infinite loop
inter-module
interface
it'd be nice
it's not perfectly documented
javadoc
lack of abstraction
lack of code comments
lack of cohesion
lack of documentation
lack of encapsulation
lack of generalization
lack of information hiding
lack of modularity
lack of separation of concerns
lack of test cases
lack of testing
latency
lead to huge memory allocation
leak
less verbose
literal strings
literal values
logging
magic numbers
magic strings
maintainability
maintainability issue
make it less brittle
makes it much easier
makes it very hard
minor
misleading
modularity
module dependencies
module-to-module
monolithic code
more efficient
more readable
more robust
more tests
more tightly coupled than ideal
multithreading issue
naming
need to update documentation
no longer needed
not done yet
not implemented
not supported yet
not thread safe
not used
output
patch doesn't apply cleanly
performance
please add a test
poor solution
poor way
poorly documented code
poorly structured code
poorly tested code
quick fix
race condition
reduce duplicate code
redundant
refact
refactor
refactoring
reliability
rename
repeated code
response time
robustness
scalability
scalability issue
short term solution
should be updated to reflect
should improve a bit by
simplify
solution won't be really satisfactory
some holes in the doc
spaghetti code
speed
speed up
spurious error messages
suboptimal solution
suboptimal way
support for
synchronization issue
system dependencies
system design problem
takes a long time
technical debt
technical debt due to architectural issues
technical debt due to design issues
technical kludge
temporary solution
test
test doesn't add much value
testing debt
there is no unit test
throughput
tidy up
tight coupling
too long
too much
trustworthiness
typo
ugly
undocumented code
undocumented strings
undocumented values
unnecessary
unreliable code
unstable
untested code
unused
unused code
unused import
update
violation
wastes a lot of space
work in progress
workaround
would significantly improve
wrong solution
wrong way
```

## Answer3 (S1A3): 
```bash
The list of SATD keywords you provided is quite extensive and covers a wide range of issues and areas where technical debt can accumulate in software projects. Developers often use these keywords to flag areas that require improvement, refactoring, or attention. Here are a few key points about these SATD keywords:

Diverse Range of Issues: The list includes keywords related to code quality, architectural issues, design flaws, documentation, performance problems, testing, and various other aspects of software development. This diversity highlights the multifaceted nature of technical debt.

Documentation: Several keywords indicate the importance of proper documentation, such as "lack of documentation," "documentation debt," and "documentation doesn't match." Insufficient or outdated documentation can be a significant source of technical debt.

Code Smells: Keywords like "code smell" and "design smell" are used to flag areas where the codebase might not adhere to best practices or could benefit from refactoring. Identifying and addressing code smells is crucial for maintaining code quality.

Testing Debt: Phrases like "no longer needed," "not used," or "no unit test" indicate the need for testing and test coverage improvements. Inadequate test coverage can lead to technical debt related to reliability and maintainability.

Performance and Scalability: Terms like "performance," "scalability issue," and "inefficient solution" draw attention to areas where the software may not meet performance expectations. These issues can accumulate technical debt in terms of system efficiency and responsiveness.

Architectural and Design Debt: Keywords like "architectural debt" and "design flaw" highlight that architectural and design decisions can contribute to technical debt. These decisions should be revisited to ensure long-term maintainability and scalability.

Communication: Some SATD keywords, such as "poorly documented code" or "spurious error messages," underscore the importance of clear communication and user-friendly error handling in software development.

Prioritization: Developers and teams can use these keywords to prioritize and plan their work. Issues marked with these keywords should be addressed over time to reduce technical debt.

Continuous Improvement: Regularly addressing issues tagged with these keywords is part of a continuous improvement process in software development. It helps prevent the accumulation of technical debt and keeps the codebase in good shape.

In practice, using SATD keywords in code comments or within an Issue Tracker System, as mentioned earlier, is an effective way to track and manage technical debt, ensuring that it doesn't impede the progress of the software project and that code quality is maintained over time.
```

## Prompt4 (S1P4):
```bash
# Stage 1 #
## Issues samples ##
### Issues types ###
Here, we can see an example of issue from Jira Apache Cassandra, that contains issue_type, summary, description and comments:

issue_type: Improvement

summary: Added support for type VECTOR<type, dimension> 

description: Based off several mailing list threads (see "[POLL] Vector type for ML”, "[DISCUSS] New data type for vector search”, and "Adding vector search to SAI with heirarchical navigable small world graph index”), its desirable to add a new type “VECTOR” that has the following properties

1) fixed length array
2) elements may not be null
3) flatten array (aka multi-cell = false) 

status: Resolved

comments: having a hard time fixing CQL3TypeLiteralTest as this test never tested what CQL supports, but tests against a model generated by a human... when you fix bugs in toCQLLiteral so it actually works in CQL, this test breaks... and is breaking in annoying ways... one way is that UDT does not allow NULL for a counter type, but this test makes sure we convert it to "name: null"... there have been a lot more... so will take time to fix this test... its also kinda the same as the new AbstractTypeTest.serde as it tests the same behavior, but uses CQL parsing to validate
A note on the serialization format: right now we're serializing vectors as just a sequence of the underlying subtypes.  So if we have a vector of floats of dimension 3 we just write three serialized floats one after another on the wire; there's no size information included for either the number of elements in the list or the size of any one element.  This differs from how other collections (such as lists and maps) and UDTs are handled.  In those cases we send along (a) the element size of a given collection and (b) the size of each element (included in the bytes structure).

Such a change isn't unreasonable, at least not for fixed size types (and perhaps the variable types as well) since hypothetically the codecs should be aware of how big a given type might be.  But that's not what, say, the Java driver does at the moment.  Let's take the example of a float type; when decoding a ByteBuffer expected to contain an instance of this type we expect that ByteBuffer to contain precisely four bytes.  The assumption is that something upstream has pulled off exactly the expected number of bytes from some larger ByteBuffer.

I certainly can take steps to expose the expected number of bytes for a given codec.  But it did seem worthwhile to highlight the difference and make sure that this difference in serialization formats represents an explicit choice.
bq. But it did seem worthwhile to highlight the difference and make sure that this difference in serialization formats represents an explicit choice.

Yes, this was something I explicitly did.  My argument was that the common case are vectors of numbers, so by optimizing for this case we save a lot of space for these vectors (vector<byte, 1024> is 1,024 bytes with this format, but would have been 5,120 if we included size).  This gets even worse if you move from a vector to a matrix (vector<vector<byte, 1024>, 1024> would be 1,048,576 bytes without the header and 20,971,520 with the header); notice that in this case vector is fixed length if-and-only-if the element type is fixed length!

One added change I have been thinking about is "fixing" ShortType to be fixed length in this code path without changing existing code paths... right now ShortType is serialized as int header + 2 byte short in vector type, but also in normal SSTable format!  Its actually cheaper for users to store a short as an int as that is stored as 4 bytes only... Given this is a new type, I could add and use a new method "valueLengthIfFixedNoForRealThisTime" and only fix ShortType to return 2 where as valueLengthIfFixed currently returns -1 (aka not fixed length)...
just pushed a patch that breaks AbstractTypeTest as I added support for CompositeType and found a fun bug where using this may corrupt the DB's in-memory state (if set<'CompositeType(...)'> is seen before set< bytes> is seen, then ordering breaks in org.apache.cassandra.serializers.SetSerializer#serializeValues... adding a test to detect this type of bug also found the same issue with LexicalUUIDType and uuid, which can corrupt ordering as well...
all types are now generated using the type builder
TIL: tinyint is variable length and not fixed length...
just found out about org.apache.cassandra.cql3.functions.types.DataType... not sure why we have duplicate logic for types yet, so need to figure out...
spoke with [~adelapena] and we are going to block vectors from being reachable fr
```

## Answer4 (S1A4):
```bash
Thank you for providing an example of an issue from Jira Apache Cassandra. Let's break down the components of this issue:

Issue Type: Improvement

The issue type indicates the nature of the task or problem. In this case, it's marked as an "Improvement," which suggests that the issue is about enhancing an existing feature or adding a new one.
Summary:

The summary provides a concise description of the issue. In this case, it mentions "Added support for type VECTOR<type, dimension>," giving a high-level overview of the improvement being proposed.
Description:

The description contains a more detailed explanation of the issue. It references discussions on the mailing list and outlines the desirable properties of a new data type called "VECTOR." It specifies properties like being a fixed-length array, non-null elements, and not being a multi-cell array.
Status:

The status indicates the current state of the issue. In this example, it is marked as "Resolved," meaning the issue has been addressed.
Comments:

The comments section contains a discussion between developers about the issue. It touches on topics like testing challenges, serialization format, codec behavior, and potential optimizations for vector types.
This example demonstrates how issues in a tracker can be diverse in nature, ranging from bug fixes to feature additions and architectural improvements. Additionally, the comments section is a valuable space for developers to collaborate, discuss challenges, and provide updates on the issue's progress.

In your project, you can leverage the information within such issues, including summaries, descriptions, and comments, to build an issue classifier capable of identifying architectural impact and technical debt within these tasks. The presence of SATD keywords in these texts can be instrumental in automating the classification process and prioritizing the handling of such issues. If you have any more questions or need further guidance, please feel free to ask.
```

# Stage 2 - Example Showcase:

We provide showcase a few sample issues (issues about task, bug-fix, improvement, and new feature) that have been converted into .txt files. These files contain issue-specific information, including issue ID, type, status, summary, description, and comments. We also mentioned that these issues have already undergone manual inspections without ChatGPT.

You can see the following prompts: S2P1..S2P11

## Prompt5 (S2P1)
```bash
# Stage 2 #
## Issues samples ##
### Issue Bug ###
Here you can see an Bug issue:

issue_type: Bug 

summary: Reuse of metadata collector can break key count calculation 

description: When flushing a memtable we currently pass a constructed {{MetadataCollector}} to the {{SSTableMultiWriter}} that is used for writing sstables. The latter may decide to split the data into multiple sstables (e.g. for separate disks or driven by compaction strategy) — if it does so, the cardinality estimation component in the reused {{MetadataCollector}} for each individual sstable contains the data for all of them.

As a result, when such sstables are compacted the estimation for the number of keys in the resulting sstables, which is used to determine the size of the bloom filter for the compaction result, is heavily overestimated.

This results in much bigger L1 bloom filters than they should be. One example (which came about during testing of the upcoming CEP-26, after insertion of 100GB data with 10% reads):
(current)
{code}
 		Bloom filter false positives: 22627369
 		Bloom filter false ratio: 0.02257
 		Bloom filter space used: 1848247864
 		Bloom filter off heap memory  

status: Open 

comments: I don't think this affects any of our current {{SSTableMultiWriter}} implementations right? {{RangeAwareSSTableWriter}} creates a new collector for every new sstable and {{SimpleSSTableMultiWriter}} only creates a single new sstable.
You are right, this currently isn't a problem here, only something to be aware of and fix / work around when a compaction strategy needs to split the flush output.

I was thinking per-disk splitting on flush can trigger this, but that's handled inside the flushing code rather than in the writer.
```

## Answer5 (S2A1):
```bash
In this example, we have an issue of type "Bug." Let's break down the components of this bug issue:

Issue Type: Bug

The issue type categorizes the nature of the problem, which, in this case, is a "Bug." Bugs typically represent unexpected behavior or issues in the software.
Summary:

The summary provides a concise description of the bug. It mentions "Reuse of metadata collector can break key count calculation," indicating the issue's core problem.
Description:

The description goes into more detail about the bug. It explains that the bug occurs when flushing a memtable and reusing a metadata collector. The issue arises when the SSTableMultiWriter decides to split the data into multiple SSTables (e.g., for separate disks or driven by a compaction strategy). The problem is that the reused MetadataCollector contains data for all of the SSTables, leading to an overestimation of the number of keys in the resulting SSTables. This, in turn, affects the size of the bloom filter used for the compaction result.
Status:

The status indicates the current state of the issue, which, in this case, is marked as "Open." This suggests that the issue has been identified but has not yet been resolved.
Comments:

The comments section contains a discussion between developers regarding the issue. They discuss the potential impact on different implementations of SSTableMultiWriter and note that the problem isn't currently an issue for some implementations. They also mention that this issue would need to be addressed when a compaction strategy requires splitting the flush output.
This bug issue highlights the importance of tracking and addressing unexpected behavior or issues in the software. It shows how developers can use issue trackers to document, discuss, and work towards resolving these problems. If you have more questions or need further information about how to handle bug issues or integrate them into your issue classifier, please let me know.
```

## Prompt6 (S2P2)
```bash
# Stage 2 #
## Issues samples ##
### Issue Improvement ###
Here you can see an improvement issue:

issue_type: Improvement 

summary: Include estimated active compaction remaining write size when starting a new compaction 

description: There are a few things we can augment in how we handle compactions locally to improve upon the very simple "keep X Mebibytes free on disk" we currently have:
 Allow specification of free space available in percent rather than raw size
 Do this on a per-disk basis based on what's going on with compactions
 Include an estimate of the disk space of active compactions in flight when we do the above calculation check so we don't blow past our limits due to concurrent runs
 
status: Resolved 

comments: ||Item|Link||
|PR|[link|https://github.com/apache/cassandra/pull/1888]|
|JDK8 CI|[link|https://app.circleci.com/pipelines/github/josh-mckenzie/cassandra/309/workflows/52b0f2a9-11f3-4cff-bbc2-2fefeca967b6]|
|JDK11 CI|[link|https://app.circleci.com/pipelines/github/josh-mckenzie/cassandra/309/workflows/c2f9dc8f-1182-42d5-92e9-1b183ba45fa3]|

Promoted writesData to member on OperationType and fixed unused import in a couple commits; CI should be running (for real) now.
```

## Answer6 (S2A2):
```bash
This example is an issue of type "Improvement" from your project, and it provides insights into how improvement-related issues are documented in your issue tracker. Let's break down the components of this improvement issue:

Issue Type: The issue is categorized as an "Improvement," indicating that it pertains to enhancing or adding new features to the software system.

Summary: The summary briefly describes the improvement. In this case, it mentions "Include estimated active compaction remaining write size when starting a new compaction," providing a concise overview of the enhancement.

Description: The description provides more detailed information about the improvement. It outlines several enhancements that can be made to how compactions are handled, such as allowing the specification of free space in percentage rather than raw size, making adjustments on a per-disk basis, and including an estimate of disk space used by active compactions when performing calculations.

Status: The issue's status is marked as "Resolved," indicating that the improvement has been addressed and implemented.

Comments: The comments section contains a series of comments and discussions related to the improvement issue. It includes links to relevant pull requests and CI pipelines, indicating that the work has been done and tested. Additionally, there is information about changes made in the codebase, such as promoting "writesData" to a member on "OperationType" and fixing an unused import.
```

## Prompt7 (S2P3)
```bash
# Stage 2 #
## Issues samples ##
### Issue New Feature ###
Here you can see an New Feature Issue:

issue_type: New Feature 

summary: On-disk string index with index building and on-disk query path 

description: An on-disk index for string (literal) datatypes. This index is used for the following datatypes:
 * UTF8Type
 * AsciiType
 * CompositeType
 * Frozen types

This includes the ability to write the index to disk at index creation, by specific index rebuild and during SSTable compaction. 

Also the ability to query the on-disk index and combine the results with those from the in-memory indexes created by CASSANDRA-18058. 

status: Resolved 

comments: The PR for this patch is here: https://github.com/maedhroz/cassandra/pull/9
Minor note: I had forgotten to actually push the trunk rebase for the CASSANDRA-16052 feature branch on the 19th. That's done, so the branch here will need a quick rebase.
I have rebased the CASSANDRA-18062 against the rebased CASSANDRA-16052 branch.
[~mfleming] Just to be clear, this is almost certainly not going to land in any 4.x release, and if [~mike_tr_adamson] is okay w/ it, I’d suggest we just use the NA version here and later inherit the main CEP-7 version when that’s finalized in the epic Jira/ticket.
[~maedhroz] Sure can do. I was just monkeying about with the versions to create a simpler kanban board, but I'm happy to use NA here.
[~mike_tr_adamson] [~adelapena] I've thrown my +1 on the PR

There are a number of Jiras we've agreed to spin off and handle separately, so modulo getting those created and making sure we're clean on tests (I can rebase if we have things failing because of trunk divergence...let me know), things are looking pretty good here.
Changes look good to me too, I have only left a few final nits on the PR.

As for testing, there are too many modified files for the automatic CircleCI repeated runs but I can start a few runs repeating the modified tests in batches. It might be preferable to do so after rebase, if we are going to rebase now.
This is the latest test run on [CircleCI|https://app.circleci.com/pipelines/github/mike-tr-adamson/cassandra/129/workflows/ffae16e7-9b23-42ef-8d6f-f47aafcb6a4b]. The failures seem unrelated to SAI so I don't whether rebase first of merge first. I'm happy with either.
Just reviewed the last clean-up commit.

+1 overall

Let's squash it, fix up the commit message, and merge this thing!

Once it's merged, I'll rebase the 16052 branch, run the tests, and report back.
I think we should run the repeated tests before merging, so we make sure we don't introduce new flakies.

I have started part of the repeated runs [here|https://app.circleci.com/pipelines/github/adelapena/cassandra?branch=18062-trunk-test]. Each push on that branch is for running a subset of the new or modified tests.

So far it has hit test failures on [{{StorageAttachedIndexDDLTest.concurrentTruncateWithIndexBuilding}}|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/workflows/8301fcae-ab73-401d-ae26-d3e7e8b0f237/jobs/38519/tests] and [{{CompactionTest.testConcurrentIndexDropWithCompaction}}|https://app.circleci.com/pipelines/github/adelapena/cassandra/2828/workflows/c22d9dc8-9af1-493f-9e13-e91631fd2386/jobs/38538/tests]. I'll keep running the rest of the tests to see if there are more flakies.
Even if we do have a couple flakes, they're only merging to the 16052 umbrella branch, where I'd be running the repeats again after the next trunk rebase. If they're trivial to resolve now before merge though, that's fine too.
These are the new flaky tests once all the CI runs have finished:
 * [o.a.c.distributed.test.sai.IndexAvailabilityTest#verifyIndexStatusPropagation|https://app.circleci.com/pipelines/github/adelapena/cassandra/2826/workflows/e63df64f-9821-4bae-add4-7b3169c50344/jobs/38621/tests]
 * [o.a.c.index.sai.cql.DecimalLargeValueTest#runQueriesWithDecimalValueCollision|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/workflows/8301fcae-ab73-401d-ae26-d3e7e8b0f237/jobs/38550/tests]
 * [o.a.c.index.sai.cql.MixedIndexImplementationsTest#shouldRequireAllowFilteringWithOtherIndex|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/workflows/06a9ee70-d522-45ab-b5f1-b18eed4818d6/jobs/38664/tests]
 * [o.a.c.index.sai.cql.StorageAttachedIndexDDLTest#concurrentTruncateWithIndexBuilding|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/workflows/8301fcae-ab73-401d-ae26-d3e7e8b0f237/jobs/38519/tests]
 * [o.a.c.index.sai.cql.StorageAttachedIndexDDLTest#verifyRebuildCorruptedFiles|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/workfl
```

## Answer7 (S2A3)
```bash
this new feature issue:

Issue Type: New Feature

The issue type categorizes the nature of the task, which, in this case, is a "New Feature." New features represent requests or proposals to add entirely new capabilities or functionalities to the software.
Summary:

The summary provides a concise description of the new feature. In this case, it mentions "On-disk string index with index building and on-disk query path," providing an overview of the proposed feature.
Description:

The description offers more detailed information about the new feature. It explains that the feature involves the creation of an on-disk index for string (literal) data types, such as UTF8Type, AsciiType, CompositeType, and Frozen types. The on-disk index is designed to be written to disk at index creation, during specific index rebuilds, and during SSTable compaction. It also outlines the capability to query the on-disk index and combine the results with those from in-memory indexes created by another related issue (CASSANDRA-18058).
Status:

The issue's status is marked as "Resolved," indicating that the new feature has been successfully implemented.
Comments:

The comments section contains various comments and discussions related to the new feature issue. It includes a link to the associated pull request (PR) and mentions the process of rebasing the branch. There are also discussions about the release version and testing processes. The comments indicate that the feature is ready for merging and further testing to address flakiness.
This new feature issue demonstrates how software development teams can track, discuss, implement, and test entirely new functionalities or capabilities within the software. It showcases the collaborative and iterative nature of software development. If you have more questions or need further information on how to manage new feature issues in your project, please feel free to ask.
```

## Prompt8 (S2P4)
```bash
# Stage 2 #
## Instructions ###
"Architectural impact" in software systems is the effect that design decisions made at the architectural level have on the system's overall quality attributes, such as performance, scalability, maintainability, security, and reliability.

Architectural impact can be both positive and negative. For example, a decision to use a microservices architecture can improve the system's scalability and maintainability, but it can also increase the system's complexity and make it more difficult to debug.

Here are some specific examples of architectural impact:

A decision to use a distributed architecture can improve the system's scalability and performance, but it can also increase the system's complexity and make it more difficult to manage.

A decision to use a layered architecture can improve the system's maintainability and security, but it can also reduce the system's performance.

A decision to use a cloud-based architecture can reduce the cost and complexity of managing the system, but it can also make the system more vulnerable to attack.
```

## Answer8 (S2A4):
```bash
Understanding "architectural impact" in software systems is crucial for assessing how design decisions at the architectural level can affect a system's overall quality attributes. These quality attributes encompass performance, scalability, maintainability, security, and reliability.

Architectural impact can take on both positive and negative dimensions. For instance, a decision to adopt a microservices architecture can enhance scalability and maintainability but may also introduce complexity and make debugging more challenging.

Here are some specific examples of architectural impact:

Distributed Architecture:

Positive Impact: Improved Scalability and Performance
Negative Impact: Increased Complexity and Management Challenges
Layered Architecture:

Positive Impact: Enhanced Maintainability and Security
Negative Impact: Potential Reduction in Performance
Cloud-Based Architecture:

Positive Impact: Reduced Cost and Simplified System Management
Negative Impact: Increased Vulnerability to Attacks
Assessing architectural impact is essential during the design and decision-making process to strike a balance between the desired quality attributes and potential drawbacks. Making informed choices is key to achieving a well-structured, efficient, and reliable software system.
```

## Prompt 9 (S2P5)
```bash
# Stage 2 #
## Architectural impact examples ###
Here are some other examples of architectural impacts in software systems:

Performance: The choice of programming language, database, and other technologies can have a significant impact on the performance of a software system. For example, a system written in a compiled language such as C++ will generally perform better than a system written in an interpreted language such as Python.

Scalability: The ability of a system to handle increased load is another important quality attribute. Some architectural decisions, such as using a distributed architecture or a cloud-based architecture, can improve the scalability of a system.

Maintainability: The ease with which a system can be modified and extended is also important. Some architectural decisions, such as using a layered architecture or a modular architecture, can improve the maintainability of a system.

Security: The ability of a system to protect itself from attack is another important quality attribute. Some architectural decisions, such as using a layered architecture or a least-privilege approach, can improve the security of a system.

Reliability: The ability of a system to operate correctly over time is also important. Some architectural decisions, such as using fault tolerance and redundancy techniques, can improve the reliability of a system.
```

## Answer9 (S2A5)
```bash
Certainly, architectural impact in software systems can manifest in various ways. Here are additional examples of architectural impacts that can influence different quality attributes:

Performance:

Choice of Technology: The selection of programming languages, databases, and frameworks can significantly impact system performance. For instance, systems built with compiled languages like C++ often exhibit better performance compared to those using interpreted languages like Python.
Algorithmic Decisions: The choice of algorithms and data structures can have a profound effect on system performance. Optimal algorithms can reduce processing time and resource consumption.
Scalability:

Distributed Architecture: Implementing a distributed architecture can enhance a system's ability to scale horizontally, accommodating increased load and users.
Cloud-Based Solutions: Leveraging cloud services can provide on-demand scalability, allowing resources to be dynamically allocated as needed.
Maintainability:

Layered Architecture: A well-structured layered architecture simplifies system maintenance by separating concerns and promoting modularity. Changes in one layer have minimal impact on others.
Modular Architecture: Modular systems enable developers to modify or extend specific components without disrupting the entire system, enhancing maintainability.
Security:

Layered Architecture: A layered architecture can contribute to security by isolating sensitive components from external access, reducing potential attack vectors.
Least-Privilege Principle: Restricting access to only the necessary resources or functionalities (least privilege) can bolster system security.
Reliability:

Fault Tolerance: Architectural choices that include fault tolerance mechanisms, such as redundancy and failover strategies, can ensure system reliability by minimizing downtime.
Redundancy Techniques: Implementing redundancy, either through hardware or software redundancy, can mitigate the impact of hardware failures and enhance system reliability.
These examples illustrate how architectural decisions can impact a software system's performance, scalability, maintainability, security, and reliability. It's essential for architects and developers to carefully consider these factors during the design and development stages to achieve the desired quality attributes while managing potential drawbacks.
```

## Prompt 10 (S2P6)
```bash
# Stage 2 #
## Instructions ##
I want a issue classifier that does not have all steps related to machine learning process, i.e, less formal, in this case, we use only contextualization, instruction and examples to analyze the content of issue (summary, description, comments) of issues. 
```

## Answer 10 (SP2P6)
```bash
Understood. In this issue classifier, we will focus on using contextualization, instructions, and examples to analyze the content of issues (summary, description, comments) without delving into the formal machine learning process. This approach will help us determine whether an issue has "Architectural Impact" or not based on the information provided in the text.

Let's proceed with analyzing the provided issues using this approach. If you have specific issues or content you'd like to start with, please provide them, and we can begin the analysis
```

## prompt 11 (S2P7)
```bash
# Stage 2 #
## Architectural impact example ##
Here is an example of issue with Architectural impact:

issue_type: New Feature

summary: On-disk string index with index building and on-disk query path 

description: An on-disk index for string (literal) datatypes. This index is used for the following datatypes:
 * UTF8Type
 * AsciiType
 * CompositeType
 * Frozen types

This includes the ability to write the index to disk at index creation, by specific index rebuild and during SSTable compaction. 

Also the ability to query the on-disk index and combine the results with those from the in-memory indexes created by CASSANDRA-18058. 
status: Resolved 
comments: The PR for this patch is here: https://github.com/maedhroz/cassandra/pull/9
Minor note: I had forgotten to actually push the trunk rebase for the CASSANDRA-16052 feature branch on the 19th. That's done, so the branch here will need a quick rebase.
I have rebased the CASSANDRA-18062 against the rebased CASSANDRA-16052 branch.
[~mfleming] Just to be clear, this is almost certainly not going to land in any 4.x release, and if [~mike_tr_adamson] is okay w/ it, I’d suggest we just use the NA version here and later inherit the main CEP-7 version when that’s finalized in the epic Jira/ticket.
[~maedhroz] Sure can do. I was just monkeying about with the versions to create a simpler kanban board, but I'm happy to use NA here.
[~mike_tr_adamson] [~adelapena] I've thrown my +1 on the PR

There are a number of Jiras we've agreed to spin off and handle separately, so modulo getting those created and making sure we're clean on tests (I can rebase if we have things failing because of trunk divergence...let me know), things are looking pretty good here.
Changes look good to me too, I have only left a few final nits on the PR.

As for testing, there are too many modified files for the automatic CircleCI repeated runs but I can start a few runs repeating the modified tests in batches. It might be preferable to do so after rebase, if we are going to rebase now.
This is the latest test run on [CircleCI|https://app.circleci.com/pipelines/github/mike-tr-adamson/cassandra/129/workflows/ffae16e7-9b23-42ef-8d6f-f47aafcb6a4b]. The failures seem unrelated to SAI so I don't whether rebase first of merge first. I'm happy with either.
Just reviewed the last clean-up commit.

+1 overall

Let's squash it, fix up the commit message, and merge this thing!

Once it's merged, I'll rebase the 16052 branch, run the tests, and report back.
I think we should run the repeated tests before merging, so we make sure we don't introduce new flakies.

I have started part of the repeated runs [here|https://app.circleci.com/pipelines/github/adelapena/cassandra?branch=18062-trunk-test]. Each push on that branch is for running a subset of the new or modified tests.

So far it has hit test failures on [{{StorageAttachedIndexDDLTest.concurrentTruncateWithIndexBuilding}}|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/workflows/8301fcae-ab73-401d-ae26-d3e7e8b0f237/jobs/38519/tests] and [{{CompactionTest.testConcurrentIndexDropWithCompaction}}|https://app.circleci.com/pipelines/github/adelapena/cassandra/2828/workflows/c22d9dc8-9af1-493f-9e13-e91631fd2386/jobs/38538/tests]. I'll keep running the rest of the tests to see if there are more flakies.
Even if we do have a couple flakes, they're only merging to the 16052 umbrella branch, where I'd be running the repeats again after the next trunk rebase. If they're trivial to resolve now before merge though, that's fine too.
These are the new flaky tests once all the CI runs have finished:
 * [o.a.c.distributed.test.sai.IndexAvailabilityTest#verifyIndexStatusPropagation|https://app.circleci.com/pipelines/github/adelapena/cassandra/2826/workflows/e63df64f-9821-4bae-add4-7b3169c50344/jobs/38621/tests]
 * [o.a.c.index.sai.cql.DecimalLargeValueTest#runQueriesWithDecimalValueCollision|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/workflows/8301fcae-ab73-401d-ae26-d3e7e8b0f237/jobs/38550/tests]
 * [o.a.c.index.sai.cql.MixedIndexImplementationsTest#shouldRequireAllowFilteringWithOtherIndex|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/workflows/06a9ee70-d522-45ab-b5f1-b18eed4818d6/jobs/38664/tests]
 * [o.a.c.index.sai.cql.StorageAttachedIndexDDLTest#concurrentTruncateWithIndexBuilding|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/workflows/8301fcae-ab73-401d-ae26-d3e7e8b0f237/jobs/38519/tests]
 * [o.a.c.index.sai.cql.StorageAttachedIndexDDLTest#verifyRebuildCorruptedFiles|https://app.circleci.com/pipelines/github/adelapena/cassandra/2835/work
```

## Answer11 (S2A7): 
```bash
 This is an example of an issue with Architectural Impact. Let's break it down:

Issue Type: New Feature

Summary: The issue is about introducing a new feature, specifically an on-disk string index with index building and on-disk query functionality.

Description: The description provides details about the new feature. It mentions the creation of an on-disk index for various string data types, including UTF8Type, AsciiType, CompositeType, and Frozen types. This index can be written to disk during index creation, specific index rebuild, and SSTable compaction. Additionally, it mentions the ability to query the on-disk index and combine results with in-memory indexes created by a previous issue (CASSANDRA-18058).

Status: The issue is marked as "Resolved," indicating that the work on this feature has been completed.

Comments: The comments section includes discussions related to the issue, such as links to the pull request (PR) for the feature, information about rebase, and decisions regarding the release version. There's also mention of running tests before merging to ensure no new test failures are introduced.

Architectural Impact: This issue has a positive architectural impact by introducing a new feature that enhances the system's capabilities. It improves the system's ability to efficiently handle on-disk string data indexing and querying, which can have a positive impact on performance, scalability, and maintainability.

This example demonstrates how architectural impact can be identified by analyzing the content of issues, even without formal machine learning processes. It involves understanding the nature of the proposed changes and their potential effects on the system's quality attributes.
```

## Prompt12 (S2P8)
```bash
# Stage 2 #
## Architectural impact example ##
Here another example of issue with Architectural impact:

issue_type: Improvement

summary: Include estimated active compaction remaining write size when starting a new compaction 

description: There are a few things we can augment in how we handle compactions locally to improve upon the very simple "keep X Mebibytes free on disk" we currently have:
 # Allow specification of free space available in percent rather than raw size
 # Do this on a per-disk basis based on what's going on with compactions
 # Include an estimate of the disk space of active compactions in flight when we do the above calculation check so we don't blow past our limits due to concurrent runs

status: Resolved 

comments: ||Item|Link||
|PR|[link|https://github.com/apache/cassandra/pull/1888]|
|JDK8 CI|[link|https://app.circleci.com/pipelines/github/josh-mckenzie/cassandra/309/workflows/52b0f2a9-11f3-4cff-bbc2-2fefeca967b6]|
|JDK11 CI|[link|https://app.circleci.com/pipelines/github/josh-mckenzie/cassandra/309/workflows/c2f9dc8f-1182-42d5-92e9-1b183ba45fa3]|

Promoted writesData to member on OperationType and fixed unused import in a couple commits; CI should be running (for real) now.
```

## Answer12 (S2A8):
```bash
Issue Type: Improvement

Summary: The issue is about improving the way compactions are handled locally. It aims to include an estimated active compaction remaining write size when starting a new compaction.

Description: The description outlines the improvements that can be made in how compactions are handled locally. The key points include:

Allowing the specification of free space available in percent rather than raw size.
Implementing these changes on a per-disk basis, based on ongoing compactions.
Including an estimate of the disk space used by active compactions in-flight when calculating the available space to prevent exceeding limits due to concurrent runs.
Status: The issue is marked as "Resolved," indicating that the proposed improvements have been implemented.

Comments: The comments section includes information about the pull request (PR) related to this issue, links to CI pipelines for testing, and details about changes made, such as promoting "writesData" to a member on "OperationType" and fixing unused imports.

Architectural Impact: This issue has a positive architectural impact by improving the system's compaction process. It enhances the way the system manages disk space during compactions, which can positively affect performance, scalability, and reliability. It ensures that the system efficiently utilizes available disk space during compaction processes, preventing potential issues related to running out of space.

This example demonstrates how architectural impact can be identified by analyzing the content of issues, even without formal machine learning processes. It involves understanding the nature of the proposed changes and their potential effects on the system's quality attributes.
```

## Prompt13 (S2P9)
```bash
# Stage 2 #
## Architectural impact example ##
Here is another issue with Architectural impact:

issue_type: Bug

summary: Reuse of metadata collector can break key count calculation 

description: When flushing a memtable we currently pass a constructed {{MetadataCollector}} to the {{SSTableMultiWriter}} that is used for writing sstables. The latter may decide to split the data into multiple sstables (e.g. for separate disks or driven by compaction strategy) — if it does so, the cardinality estimation component in the reused {{MetadataCollector}} for each individual sstable contains the data for all of them.

As a result, when such sstables are compacted the estimation for the number of keys in the resulting sstables, which is used to determine the size of the bloom filter for the compaction result, is heavily overestimated.

This results in much bigger L1 bloom filters than they should be. One example (which came about during testing of the upcoming CEP-26, after insertion of 100GB data with 10% reads):
(current)
{code}
 		Bloom filter false positives: 22627369
 		Bloom filter false ratio: 0.02257
 		Bloom filter space used: 1848247864
 		Bloom filter off heap memory  

status: Open 

comments: I don't think this affects any of our current {{SSTableMultiWriter}} implementations right? {{RangeAwareSSTableWriter}} creates a new collector for every new sstable and {{SimpleSSTableMultiWriter}} only creates a single new sstable.
You are right, this currently isn't a problem here, only something to be aware of and fix / work around when a compaction strategy needs to split the flush output.

I was thinking per-disk splitting on flush can trigger this, but that's handled inside the flushing code rather than in the writer.
```

## Answer13 (S2A9):
```bash
Description: The description highlights the problem. When flushing a memtable, a constructed MetadataCollector is passed to the SSTableMultiWriter used for writing SSTables. If the SSTableMultiWriter decides to split the data into multiple SSTables, the reused MetadataCollector for each individual SSTable contains data for all of them. This leads to incorrect cardinality estimations for the number of keys in the resulting SSTables, which are used to determine the size of the bloom filter for compaction results. This overestimation results in much larger L1 bloom filters than they should be.

Status: The issue is marked as "Open," indicating that it has not been resolved yet.

Comments: The comments section includes a discussion about the issue, with considerations regarding its impact on existing SSTableMultiWriter implementations. It is noted that the problem doesn't affect some current implementations, and it should be addressed when a compaction strategy needs to split the flush output.

Architectural Impact: This issue has a negative architectural impact on the system's performance and resource usage. The incorrect key count calculations and overestimated bloom filter sizes can lead to increased memory usage and potentially impact the system's performance during compactions. It highlights the importance of correctly managing and isolating metadata when dealing with split data in SSTables to avoid these issues.
```

## Prompt14 (S2P10)
```bash
# Stage 2 #
## Architectural impact example ##
Here is an example of issue that does not have Architectural Impact:

issue_type: Bug

summary: Mixed line endings in the codebase

description: There seems to be a lot of line endings in the codebase that end with DOS line endings. Some files are even mixes of DOS and Unix line endings. This patch removes all the DOS file endings and corrects them to Unix.

Also attached is the program that I used to remove them. 

Using Unix line endings in all places makes lots of things easier. At the very least, a consistent choice of line endings would. Has there been discussion of what should be the correct line ending to use?

status: Resolved 

comments: This is the patch file to remove the DOS line endings from the code. no.rb is a ruby program that I ran to create this patch.
Oh, and that program is so ugly because I wanted to be sure I was just replacing "\r\n" and not also adding newlines at the ends of files, etc. 
The vast majority of the files use Windows line endings, which makes sense since the original authors develop on Windows.  It makes more sense to me to standardize on that, even though I develop on Linux.
As long as we standardized on one or the other, as long as we set the svn:eol-style to native things should resolve themselves, right?  Windows users see Windows line endings and *X users see *X line endings.
I like the sound of this deep svn voodoo.
The mixed line-endings drove me nuts when developing on Windows. Cygwin made everything worse. None of the eol settings in git would do the right thing. Standardizing on one set of endings would be cause for great joy!
I had no idea that existed.  Will it deal with the few files that have mixed line endings?
I don't think it would handle them properly, although I'm not sure.  You can set individual files to one or the other, or native, but I think you'd have to leave it without an svn:eol-style if you *wanted* to keep it mixed.  It'd be better to convert them first if there's no compelling reason for them to be mixed.

http://svnbook.red-bean.com/en/1.1/ch07s02.html#svn-ch-7-sect-2.3.5 is the relevant section of the subversion book.

The algorithm would be:
 - find all files we want to have proper eol's
 - convert them all to your native system's eol's
 - for each filename in files:
 - - svn propset svn:eol-style native filename
 - commit all files

The above is obviously most easily done with a script.

To keep things nice going forward after this is done, if each committer added the following section to their .subversion/config then new files would automatically have the correct eol style set:
[auto-props]
*.java = svn:eol-style=native
*.properties = svn:eol-style=native
*.py= svn:eol-style=native
*.sh = svn:eol-style=native;svn:executable
*.thrift = svn:eol-style=native
*.txt = svn:eol-style=native
*.xml = svn:eol-style=native
I doubt the svn-magic will play well with Git.

Can we switch to Unix endings and be done with it?
The svn-magic plays just fine with Git, git-svn knows about eol-style.  Even so, people not using git-svn and just using git directly would ignore the settings.

Re: Unix endings, yeah, I was suggesting moving to Unix endings.  Settings those styles allows editors and platforms without appropriate eol handling to treat them natively though.
Unix line ending conversion done from code in r797209.

Using this code:

{code}
find . -name "*.java" -print0 -o -name "*.sh" -print0 -o -name "*.xml" -print0 -o -name "*.txt" -print0 | xargs -0 dos2unix
{code}
I don't see anyone that prefers \r\n trying to make this consistent or making noise about wanting consistency. I say the Unix hackers win this one.
Corrected unix line endings patch. Last one was an aborted one that someone was renamed. Apologies.
Since we're seeing more and more mixing of line endings (like in r798935), here is another patch moving cassandra to unix line endings. Patch is against r799140.
with a trunk cassandra-crlf and a patched cassandra-crlf2 this returns no result:
diff -r -w cassandra-crlf cassandra-crlf2

+1 for applying this immediately.  There are no enormous patches in the queue and this doesn't mess with any Windows-specific files.

I still think we should be applying the svn properties and configuration I discuss above, but getting all the files into the correct format is the most important step.
Committed.

 190 files changed, 30157 insertions(+), 30157 deletions(-)
Integrated in Cassandra #153 (See [http://hudson.zones.apache.org/hudson/job/Cassandra/153/])
    run source files through dos2unix to standardize on \n line endings.  patch by Jeff Hodges; reviewed by Michael Greene for 

Integrated in Cassandra #158
```

## Answer14 (S2A10):
```bash
Here's an example of an issue that does not have Architectural Impact:

Issue Type: Bug

Summary: The issue is related to mixed line endings in the codebase.

Description: The description points out that there are inconsistencies in line endings in the codebase. Some files have DOS line endings, and the patch is aimed at removing DOS line endings and converting them to Unix line endings. The goal is to achieve consistency in line endings throughout the codebase.

Status: The issue is marked as "Resolved," indicating that it has been addressed.

Comments: The comments section contains a discussion about the process of standardizing on Unix line endings. It includes a script used to convert files to Unix line endings and suggestions for setting Subversion properties and configurations for handling line endings. There is support for making this change to Unix line endings, and the issue is eventually committed.

Architectural Impact: This issue does not have a significant architectural impact on the system. It addresses a coding style consistency concern but does not have a direct impact on the performance, scalability, maintainability, security, or reliability of the software system. It is more of a coding practice improvement rather than an architectural change.
```

## Prompt15 (S2P11):
```bash
# Stage 2 #
## Architectural impact example ##
Here is another example of issue that does not have Architectural Impact

issue_type: New Feature

summary: Allow selecting Map values and Set elements 

description: Allow "SELECT map['key]" and "SELECT set['key']." 

status: Resolved 

comments: What should we do for "does element X exist in set Y" syntax?
Is this something for CASSANDRA-7395 ?
Want to say: wouldn't it be easier to add some "C*-UDF-stdlib" and implement it there?
The drawback: it would look like {{select stdlib:mapGet( map, 'key' ),  stdlib:listGet( list, 42 ),  stdlib:setContains( set, 'value' )  ...}}
Or add some "operator" functionality to UDF : {{+ - / * !  [x]}}
It's definitively worth having proper syntactic sugar here imo and that's really mainly what this issue is about. We can indeed make this sugar generate a function call behind the scene but we don't need CASSANDRA-7395 per-se to add such function.

Also, ultimately we can and should make those operator be "efficient" (at least for map and sets, for lists there is no much we can do) by not querying the whole CQL row if we don't need to (which amount to extending what CASSANDRA-7085 will introduce) so we'll almost surely end up with having those operation being special cased anyway, not just simple function calls.
It seems to me a natural extension would be extending this to slicing capabilities

map[key1..key2] 

or whatever syntax was appropriate.
bq. It's definitively worth having proper syntactic sugar here

agree

UDFs are not a requirement for this one - but may help to quickly add new functionality with the option to optimize that later (using CASSANDRA-7085, optimized slice queries etc)

bq. slicing capabilities map[key1..key2] 


maybe also to check which keys are present for a slice (or at all) and return these keys

and some "containsKey(key1..key2)" (return a boolean or an int with the count of the existing keys)
Proposal ("map" used for map columns, "set" for set columns, "list" for list columns) :
* {{map\[key]}} to return single map value or {{null}}
* {{map?\[key]}} tests whether single map key exists ({{true}} or {{false}})
* {{map\[key1..key2]}} to return sliced map
* {{map?\[key1..key2]}} to return set with keys that are present in the map
* {{map\[..key2]}} to return sliced map
* {{map?\[..key2]}} to return set with keys that are present in the map
* {{map\[key1..]}} to return sliced map
* {{map?\[key1..]}} to return set with keys that are present in the map
* {{set\[key]}} returns {{true}} or {{false}} whether a single element exists
* {{set\[key1..key2]}} to return sliced set (check values of multiple elements)
* {{set\[key1..]}} to return sliced set (check values of multiple elements)
* {{set\[..key2]}} to return sliced set (check values of multiple elements)
* {{list\[idx]}} to return single list element
* {{list?\[idx]}} tests whether single list element exists ({{true}} or {{false}})
* {{list\[idx1..idx2]}} to return sliced list - list has length {{idx2-idx1+1}}
* {{list?\[idx1..idx2]}} to return sliced list with {{true}} or {{false}} indicating whether an element exists (is no tnull)
* {{sizeof(map)}}, {{sizeof(set)}}, {{sizeof(list)}} to return size of map/set/list

Restriction for {{key1..key2}} : {{key1}} must be less than {{key2}}

Using these collection operations on parts of primary key columns would require special handling.
Primary key columns are stored in their serialized byte representation - so it would need deserialzation, handling, 2nd serialization.

All would be added to {{unaliasedSelector}} in {{Cql.g}}.
Other thoughts?

I've built a POC for slicing (except {{sizeof}} functions) availabile at github at https://github.com/snazy/cassandra/tree/7396-coll-slice to illustrate functionality. 

That POC does not use column slicing to read only the requested values. In fact I do not know how to read only a map key „foobar“ from a table with clustering keys. AFAIK will the "internal column name“ something like "clusteringKey:mapColumnName:mapColumnKey“. Such a read optimization could be done for tables that not not have a clustering key.

But there’s room for optimization to prevent unnecessary internal serialization-deserialization-serialization sequences for the above collection operations by using only  
```

## Answer15 (S2A11): 
```bash
Here's an example of an issue that does not have Architectural Impact:

Issue Type: New Feature

Summary: The issue is about allowing the selection of Map values and Set elements in queries.

Description: The description suggests allowing the use of "SELECT map['key]" and "SELECT set['key']." This feature would enable users to retrieve specific map values or set elements directly in queries.

Status: The issue is marked as "Resolved," indicating that the new feature has been implemented.

Comments: The comments section contains a discussion about the syntax and functionality of the proposed feature. It includes considerations about using User-Defined Functions (UDFs) and optimizing the operations. There are suggestions and proposals for extending the feature to include slicing capabilities and checks for the existence of keys in maps and elements in sets. The discussion also mentions building a proof of concept (POC) to illustrate the functionality.

Architectural Impact: This issue does not have a significant architectural impact on the system. It introduces a new feature for querying specific elements within collections (maps and sets) but does not fundamentally alter the system's architecture. The proposed feature is more related to query language improvements and does not directly impact performance, scalability, maintainability, security, or reliability of the software system.
```

# Stage 3 (Data Preparation) involves the manual selection of issues to be inspected.

Input Set: List of .txt files containing detailed issue information.

# Stage 4 (Final instruction to start the inspection by ChatGPT)

The last prompt to be executed before start the semi-automatic inspection.

## Prompt 16 (S4P1)
```bash
# Stage 4 #
# Instruction #
Now,  in the Stage 4 (Issue classifier) is responsable to analyze each issue using the summary, description and comments of issue to check if there is "Architectural impact" or does not have "Architectural Impact" in the software. Also, it is necessary to justify the answer based on content of issue about architectural impact. You can also add a label Archictural Impact:Yes if the issues has architectural impact or label Architectural Impact:No. After the justification of Architectural Impact.
```

# Using the model 

After setup the "model" with prompts aforementioned, you can pass the content of the issue, copy answer from ChatGPT and save the result of inspection by ChatGPT in a .txt file.

# Overview Validation Process 

## Data Preparation:

We generated individual .txt files for each of the 163 issues for inspection. Each file should contain detailed issue information, including issue ID, type, status, summary, description, and comments.

## Manual Inspection

The 163 issues are selected for manual inspection. We saved the results of these manual inspections in 163 separate .txt files to be evaluated in other stage.

## ChatGTP Inspection

We utilized ChatGPT to inspect each of the 163 .txt files representing issues. The primary goal is to identify potential architectural impacts, architectural issues, and/or technical debt within the analyzed issues. Also we requested justification for each inspection. Finally, we saved the results of these ChatGPT inspections in 163 separate .txt files to be evaluated in other stage.

## Manual Review:

Finally, in the last stage we conducted a manual review of all 163 sets of inspection results (.txt files) both manual inspection and inspection by ChatGPT. Cohen's Kappa coefficient is calculated to compare the agreement between the results obtained in the manual inspection and inspection by ChatGPT. This helps assess the consistency between manual and automatic inspections, contributing to a precise analysis of the relationship between critical issues and their impact on the software's architecture.
