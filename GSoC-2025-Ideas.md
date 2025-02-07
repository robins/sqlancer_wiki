# Contributor Guidance

When reaching out to us, please understand that we might not respond to overly generic messages that could be sent to any of the GSoC organizations. We appreciate specific and informed requests, thoughts, or ideas.

To maximize your chance of submitting a successful proposal, we recommend the following:
* Read the [GSoC student guide](https://google.github.io/gsocguides/student/).
* Go through the SQLancer resources, in particular, the [CONTRIBUTING.md](https://github.com/sqlancer/sqlancer/blob/master/CONTRIBUTING.md) document as well as the [SQLancer YouTube tutorial](https://www.youtube.com/playlist?list=PLm7ofmclym1E2LwBeSer_AAhzBSxBYDci).
* Join the [SQLancer Slack](https://join.slack.com/t/sqlancer/shared_invite/zt-eozrcao4-ieG29w1LNaBDMF7OB_~ACg), which is the main means of communication used by the SQLancer developers, and introduce yourself. We also encourage you to share your ideas with us using this platform, so we can support you with your proposal.
* It would significantly strengthen your case if you could show your aptitude by finding an opportunity to create one or multiple PRs. Refactorings would be a low-hanging fruit. For example, you could factor out common functionality in statement generators [like in a previous PR for `UPDATE` SQL statements](https://github.com/sqlancer/sqlancer/pull/662). As another example, you could [update an outdated database system version](https://github.com/sqlancer/sqlancer/blob/main/README.md#faq).

# Projects Ideas

## Adding Grammars to Test New Database Systems

SQLancer supports close to 20 database systems (see the subdirectories with the relevant database names at [src/sqlancer](https://github.com/sqlancer/sqlancer/tree/master/src/sqlancer)). Adding support for a new database system involves developing generators that generate SQL statements specific to the database system under test. The process of adding a new database system is described in the [CONTRIBUTING.md](https://github.com/sqlancer/sqlancer/blob/master/CONTRIBUTING.md#implementing-support-for-a-new-dbms) guide.

Recently, we have developed a new domain-specific language called [SQL Generation Language (SGL)](https://github.com/albertZhangTJ/sqlancer-lancerfuzz/tree/grammar_optimization/src/lancerfuzz) which should be used to aid you with this process. SGL takes in a grammar file that describes syntaxes of the target SQL dialect. The language is designed based on [ANTLR](antlr.org) which describes context-free grammars (to be exact, parser expression grammars) for parsing, on top of which language constructs for maintaining fuzzing contexts and enforcing semantic constraints are added. 

* **Required skills**: Experience with using Git as well as basic SQL knowledge is expected
* **Expected size**: Either 175 or 350 hour
* **Difficulty**: Medium
* **Expected outcomes**: Support for one (or multiple) new database systems as well as reporting of bugs found in that system
* **Potential mentors**: [@albertZhangTJ](https://github.com/albertZhangTJ)

Various additional hints:

* Most implementations use JDBC, which is well-supported by SQLancer.
* To get an idea of what database systems you could consider supporting, the [DB-Engines ranking](https://db-engines.com/en/ranking/relational+dbms) or the [Database of Databases](https://dbdb.io/) might be useful.
* It would be useful to first contact the developers of the database system to check whether they would welcome a testing effort of their system.
## Adding a Feedback-guided Fuzzing Approach

Currently, the main approach used by SQLancer to generate test cases is generation-based and black-box. The goal of this project is to add mutation-based fuzzing support to SQLancer. To this end, random decisions in the generators (mostly implemented in the [Randomly class](https://github.com/sqlancer/sqlancer/blob/8f4966a1b67dff22951f2bf3e0a02ad301fb86f1/src/sqlancer/Randomly.java)) should be recorded as seed inputs (so-called [decision seeds](https://arxiv.org/pdf/2109.11277)), and further mutated. Different ways of measuring whether a test input triggers an interesting behavior should be tried and experimented with; for example, [query plans are one potential feedback signal](https://arxiv.org/pdf/2312.17510).

* **Required skills**: Strong Java skills are essential and experience with using Git as well as basic SQL knowledge is expected
* **Expected size**: Either 175 or 350 hour
* **Difficulty**: Medium
* **Expected outcomes**: Initial prototype that can be merged into the main SQLancer repository
* **Potential mentors**: [@albertZhangTJ](https://github.com/albertZhangTJ)
