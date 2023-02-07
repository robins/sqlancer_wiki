# Contributor Guidance

When reaching out to us, please understand that we might not respond to overly generic messages that could be sent to any of the GSoC organizations. We appreciate specific and informed requests, thoughts, or ideas.

To maximize your chance of submitting a successful proposal, we recommend the following:
* Read the [GSoC student guide](https://google.github.io/gsocguides/student/).
* Go through the SQLancer resources, in particular, the [CONTRIBUTING.md](https://github.com/sqlancer/sqlancer/blob/master/CONTRIBUTING.md) document.
* Join the [SQLancer Slack](https://join.slack.com/t/sqlancer/shared_invite/zt-eozrcao4-ieG29w1LNaBDMF7OB_~ACg), which is the main means of communication used by the SQLancer developers, and introduce yourself. We also encourage you to share your ideas with us using this platform, so we can support you with your proposal.
* It would significantly strengthen your case if you could show your aptitude by finding an opportunity to create one or multiple PRs. Refactorings would be a low-hanging fruit. For example, you could factor out common functionality in statement generators [like in a previous PR for `UPDATE` SQL statements](https://github.com/sqlancer/sqlancer/pull/662). As another example, you could [update an outdated database system version](https://github.com/sqlancer/sqlancer#i-am-running-sqlancer-on-the-latest-version-of-a-supported-dbms-is-it-expected-that-sqlancer-prints-many-assertionerrors).

# Projects Ideas

## Adding Support for and Testing New Database Systems

SQLancer supports close to 20 database systems (see the subdirectories with the relevant database names at [src/sqlancer](https://github.com/sqlancer/sqlancer/tree/master/src/sqlancer)). Adding support for a new database system involves writing generators that generate SQL statements specific to the database system under test. The process of adding a new database system is described in the [CONTRIBUTING.md](https://github.com/sqlancer/sqlancer/blob/master/CONTRIBUTING.md#implementing-support-for-a-new-dbms) guide.

The goal of this project could be to add support for one or multiple database systems, and test the systems aiming to report bugs to their developers. A key consideration when selecting a database system is to ensure that the developers of the system welcome bug reports and are actively fixing them. After gaining experience with adding support for a new database system, a secondary goal could be to make it easier to add additional database systems by refactoring parts of SQLancer. For example, most of the [TestOracle](https://github.com/sqlancer/sqlancer/blob/9275f1ddd1d3bb33c1a10f07f41ecf9b552fdfbd/src/sqlancer/common/oracle/TestOracle.java) have duplicated code, which could be unified.

* **Expected outcomes**: Contributors are likely to add one or more testing implementations to SQLancer while being able to find and report bugs to database system developers (which can be exciting and addictive!). An optional outcome might be that refactorings make it easy to add new testing implementations in the future.
* **Required skills**: Strong Java skills are essential and experience with using Git as well as basic SQL knowledge is expected
* **Expected size**: Either 175 or 350 hour
* **Difficulty**: Medium
* **Possible mentors**: [Anxing Zhang](https://github.com/SuriZhang), [Jinsheng Ba](http://jinshengba.me/)

Various additional hints:

* Most implementations use JDBC, which is well-supported by SQLancer.
* To get an idea of what database systems you could consider supporting, the [DB-Engines ranking](https://db-engines.com/en/ranking/relational+dbms) or the [Database of Databases](https://dbdb.io/) might be useful.
* It would be useful to first contact the developers of the database system to check whether they would welcome a testing effort of their system.


## SQLancer Website

SQLancer lacks a project website. The goal of this project would be to create one. Pages could be created to visualize currently-supported database systems, a collection of resources, and a short tutorial. Optionally, statistics and graphs could be computed and visualized about bugs that have been found. An incomplete list is found in a [bugs.json](https://github.com/sqlancer/bugs/blob/master/bugs.json) file, and additionally, GitHub could be crawled to find [issue reports related to SQLancer](https://github.com/search?q=sqlancer).

* **Expected outcomes**: This project is expected to lead to a project website hosted on a platform such as [GitHub Pages](https://pages.github.com/)
* **Required skills**: Knowledge and experience with existing web technologies are expected; knowledge of a scripting language such as Python would be useful to visualize the bugs found by SQLancer
* **Expected size**: Either 175 or 350 hour
* **Difficulty**: Medium
* **Possible mentors**: [Manuel Rigger](https://github.com/mrigger)

## Test Case Reduction

SQLancer randomly generates test cases consisting of potentially hundreds or thousands of SQL statements. Once a bug is found, it is time-consuming to identify those SQL statements that are relevant for reproducing the bug. The goal of this project is to add automatic reduction support to SQLancer; once a bug is found, statements are systematically removed until a minimal bug-inducing test case is derived. Further explanation and a proof-of-concept implementation are included or linked to in an existing issue at [#333](https://github.com/sqlancer/sqlancer/issues/333).

* **Expected outcomes**: This project will add reduction capability to SQLancer, which will save a lot of time for developers
* **Required skills**: Strong Java skills are essential and experience with using Git as well as basic SQL knowledge is expected
* **Expected size**: Either 175 or 350 hour
* **Difficulty**: Medium
* **Possible mentors**: [Yichen Yan](https://www.linkedin.com/in/yichen-yan-222250102/), [Chi Zhang](https://ch1zhang.github.io/)


## Support Query Plan Guidance for More Database Systems

[Query Plan Guidance (QPG)](http://jinshengba.me/assets/pdf/qpg_icse23.pdf) is a test case generation method that is guided by query plans. QPG has been integrated into SQLancer ([#641](https://github.com/sqlancer/sqlancer/issues/641)) and supports SQLite, TiDB, and CockroachDB. The goal of this project is to support QPG for other database systems in SQLancer. The core general logic of QPG is in [ProviderAdapter.java](https://github.com/sqlancer/sqlancer/blob/9275f1ddd1d3bb33c1a10f07f41ecf9b552fdfbd/src/sqlancer/ProviderAdapter.java#L115-L259), and each specific database system is required to implement three interface functions, such as the implementation for [SQLite](https://github.com/sqlancer/sqlancer/blob/9275f1ddd1d3bb33c1a10f07f41ecf9b552fdfbd/src/sqlancer/sqlite3/SQLite3Provider.java#L307-L347).

* **Expected outcomes**: This project will add QPG support for other database systems, such as MySQL, and PostgreSQL
* **Required skills**: Strong Java skills are essential. Experience with using Git as well as basic SQL knowledge is expected
* **Expected size**: Either 175 or 350 hour
* **Difficulty**: Medium
* **Possible mentors**: [Jinsheng Ba](http://jinshengba.me/)