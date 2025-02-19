# Contributor Guidance

When reaching out to us, please understand that we might not respond to overly generic messages that could be sent to any of the GSoC organizations. We appreciate specific and informed requests, thoughts, or ideas.

To maximize your chance of submitting a successful proposal, we recommend the following:
* Read the [GSoC student guide](https://google.github.io/gsocguides/student/).
* Go through the SQLancer resources, in particular, the [CONTRIBUTING.md](https://github.com/sqlancer/sqlancer/blob/master/CONTRIBUTING.md) document.
* Join the [SQLancer Slack](https://join.slack.com/t/sqlancer/shared_invite/zt-eozrcao4-ieG29w1LNaBDMF7OB_~ACg), which is the main means of communication used by the SQLancer developers, and introduce yourself. We also encourage you to share your ideas with us using this platform, so we can support you with your proposal.
* It would significantly strengthen your case if you could show your aptitude by finding an opportunity to create one or multiple PRs. Refactorings would be a low-hanging fruit. For example, you could factor out common functionality in statement generators [like in a previous PR for `UPDATE` SQL statements](https://github.com/sqlancer/sqlancer/pull/662). As another example, you could [update an outdated database system version](https://github.com/sqlancer/sqlancer#i-am-running-sqlancer-on-the-latest-version-of-a-supported-dbms-is-it-expected-that-sqlancer-prints-many-assertionerrors).

# Projects Ideas

## User Interface for SQLancer

SQLancer's user interface is limited by printing regular status update to the command line. The goal of this project is to make SQLancer more user-friendly by creating a better user interface or a bug management tool. This interface could be implemented in various ways. For example, it could take [inspiration from AFL](https://en.wikipedia.org/wiki/American_Fuzzy_Lop_%28software%29#/media/File:American_fuzzy_lop's_afl-fuzz_running_on_a_test_program.png) by creating a better command line interface. As another example, it could take inspiration from [syzkaller's web interface](https://syzkaller.appspot.com/upstream) to manage the bugs that were found.

* **Required skills**: Strong Java skills are essential and experience with using Git as well as basic SQL knowledge is expected. In addition, this project requires experience with creating user interfaces.
* **Expected size**: 350 hours
* **Difficulty**: Medium
* **Expected outcomes**: A working prototype for a new user interface
* **Potential mentors**: [@suyZhong](https://github.com/suyZhong)

## Updating SQLancer to the Latest Database System Versions

SQLancer supports more than 20 database systems through custom SQL generators. However, many of these implementations are outdated. For example, the current MySQL that is support is version [8.30.0](https://github.com/sqlancer/sqlancer/blob/3e960fb16fac42ed8f43eecf25eb4d09a5be9d85/pom.xml#L307), while the latest version is [8.36.0](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-36.html). Similarly, many of our [CI tests](https://github.com/sqlancer/sqlancer/blob/3e960fb16fac42ed8f43eecf25eb4d09a5be9d85/.github/workflows/main.yml) have become outdated and fail due to various reasons. The goal of this project is to update SQLancer so it can be applied to the latest versions of these systems. In the process, new bugs will likely be discovered, which should be reported to the developers of the database systems.

* **Required skills**: Strong Java skills are essential and experience with using Git as well as basic SQL knowledge is expected
* **Expected size**: Either 175 or 350 hour
* **Difficulty**: Easy
* **Expected outcomes**: Updating support for most of the (around 20) database systems to the latest version, and reporting any new bugs in them that are found in the process
* **Potential mentors**: [@malwaregarry](https://github.com/malwaregarry)

## Adding Support for and Testing New Database Systems

SQLancer supports close to 20 database systems (see the subdirectories with the relevant database names at [src/sqlancer](https://github.com/sqlancer/sqlancer/tree/master/src/sqlancer)). Adding support for a new database system involves writing generators that generate SQL statements specific to the database system under test. The process of adding a new database system is described in the [CONTRIBUTING.md](https://github.com/sqlancer/sqlancer/blob/master/CONTRIBUTING.md#implementing-support-for-a-new-dbms) guide.

The goal of this project could be to add support for one or multiple database systems, and test the systems aiming to report bugs to their developers. A key consideration when selecting a database system is to ensure that the developers of the system welcome bug reports and are actively fixing them. After gaining experience with adding support for a new database system, a secondary goal could be to make it easier to add additional database systems by refactoring parts of SQLancer. For example, most of the [TestOracle](https://github.com/sqlancer/sqlancer/blob/9275f1ddd1d3bb33c1a10f07f41ecf9b552fdfbd/src/sqlancer/common/oracle/TestOracle.java) have duplicated code, which could be unified.

* **Required skills**: Strong Java skills are essential and experience with using Git as well as basic SQL knowledge is expected
* **Expected size**: Either 175 or 350 hour
* **Difficulty**: Medium
* **Expected outcomes**: Support for one (or multiple) new database systems as well as reporting of bugs found in that system
* **Potential mentors**: [@malwaregarry](https://github.com/malwaregarry)

Various additional hints:

* Most implementations use JDBC, which is well-supported by SQLancer.
* To get an idea of what database systems you could consider supporting, the [DB-Engines ranking](https://db-engines.com/en/ranking/relational+dbms) or the [Database of Databases](https://dbdb.io/) might be useful.
* It would be useful to first contact the developers of the database system to check whether they would welcome a testing effort of their system.

## Finer Control of Features Used in Queries

Individual SQLancer database system implementations currently provide options to control what features are included in statements and queries generated for these database system. For example, the SQLite implementation provides a [``--test-functions`` option](https://github.com/sqlancer/sqlancer/blob/3e960fb16fac42ed8f43eecf25eb4d09a5be9d85/src/sqlancer/sqlite3/SQLite3Options.java#L62) that controls whether expressions can include function calls. The goal of this project is to introduce a common set of options that is used by every system, similar to the [`--max-expression-depth` option](https://github.com/sqlancer/sqlancer/blob/3e960fb16fac42ed8f43eecf25eb4d09a5be9d85/src/sqlancer/MainOptions.java#L35) that is currently supported by all (or most) database system implementations. Introducing such options will also require improving other parts of the codebase, to enforce that new implementations implicitly make use of these options.

* **Required skills**: Strong Java skills are essential and experience with using Git as well as basic SQL knowledge is expected
* **Expected size**: Either 175 or 350 hour
* **Difficulty**: Easy
* **Expected outcomes**: A unified set of options supported by all database system implementations
* **Potential mentors**: [@suyZhong](https://github.com/suyZhong)

## Adding Support for Adding an External Reducer

The aim of this project is to enhance SQLancer by incorporating support for storing associated interestingness tests along with reported test cases, which is needed to support external test-case reducers. SQLancer already has its own built-in [reducers](https://github.com/sqlancer/sqlancer/blob/main/src/sqlancer/Reducer.java), such as [ASTBasedReducer](https://github.com/sqlancer/sqlancer/blob/main/src/sqlancer/ASTBasedReducer.java) and [StatementReducer](https://github.com/sqlancer/sqlancer/blob/main/src/sqlancer/StatementReducer.java), which minimize bug-inducing test cases that are found, but they are tightly integrated into its system, making it challenging to use and compare their efficiency with existing reducers like [creduce](https://github.com/csmith-project/creduce), which might be effective in reducing a wide range of SQL dialects and other query languages. 

To address this, the project will implement a method for SQLancer to not only output test cases but also provide their associated interestingness tests. The format of the interestingness test will be designed to seamlessly integrate with popular existing tools like creduce, vulcan, and perses (in that order of priority), out of the box.

- **Required skills**: Strong Java skills are essential and experience with using Git as well as basic SQL knowledge is expected
- **Expected size** : 175
- **Difficulty**: Medium
- **Expected outcomes**: Support for storing the interestingness test in a format that can be easily utilized with external reducers.
- **Potential mentors**: [@mzfr](https://github.com/mzfr)