# 0x435 Search Engine

## Search Log Analysis

**query session** (search session) is a sequence of query submitted by one unique user within a short time of interval

### Query Suggestion

20% of all searches are unique, 97% of all searches occur less than 10 times

#### Pseudo Document

For a search trail $(q_1, q_2, ..., q_n)$. Under the assumption $q_n$ corresponds to the actual user's intent. Create a pseudo document with $q_n$ as the title, $(q_1, ..., q_{n-1})$ as the body. To get a suggestion, start a new query into this pseudo documents and return the title.

#### Co-occurrence

Suggestions based on the co-occurrence within the same search session. Its disadvantage is data sparsity and cannot deal with long-tail queries

Rank the suggested query with $Count(q_s)$ and $Count(q, q_s)$ where $Count(q_s)$ is the popularity of suggested query and $Count(q, q_s)$ is the count of co-occurrence of $q_s$ follow the user's actual query $q$ in the search session. looks like Bayesian approach.

## Reference

[1] CMU 11-642 [https://boston.lti.cs.cmu.edu/classes/11-642/](https://boston.lti.cs.cmu.edu/classes/11-642/)

[2] Manning, Christopher D., Prabhakar Raghavan, and Hinrich Schütze. _Introduction to information retrieval_. Cambridge university press, 2008.