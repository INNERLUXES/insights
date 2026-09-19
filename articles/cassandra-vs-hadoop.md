# Cassandra vs Hadoop (HDFS): what we check before we recommend one

Canonical version: https://innerluxes.dev/data/cassandra-vs-hadoop

The feature tables tell you what each system can do. They do not tell you which one your project needs. When a client
sends us a data platform brief, these are the checks we run before either name comes up.

## Start from the query, not the technology

Write down the five most important questions the system has to answer, and how fast. "Show this customer's last 50
events" is a key lookup that has to come back in milliseconds. "Compare this quarter's usage by region against last
year's" is a scan across most of the data set that can take minutes. The first is what Apache Cassandra is built for.
The second is what HDFS with a batch engine such as Spark or Hive is built for. Most disagreements about Cassandra vs
Hadoop disappear once the team agrees which of those two lists is longer.

## Cassandra is modelled around queries, and that has a cost

In Cassandra you design one table per query pattern and repeat the data across tables when you need a second access
path. That makes reads fast and predictable, and it is why Cassandra is a poor fit for exploratory work where nobody
knows the questions yet. Deletes and TTLs leave tombstones that reads still have to skip until compaction clears them,
so a table that is written and deleted heavily needs deliberate design. If the team has not worked with a
partition-key model before, budget time for it. It is the most common reason a first Cassandra project stalls.

## HDFS and the small files problem

HDFS keeps the file system metadata in the NameNode's memory, so millions of tiny files cost far more than a few large
ones. Streaming data that lands as a file per event or per minute has to be compacted into larger files (Parquet or ORC
is the usual choice) before it is queried. It is a routine job, but it belongs in the design from the start.

## Consistency you tune versus consistency you inherit

Cassandra lets you choose the consistency level per query: ONE for a fast read that can be slightly stale, a quorum
when the answer has to be current. That flexibility moves a decision onto the application team. HDFS files are written
once and read many times, so the question hardly arises. If the data is financial or clinical and the team wants one
rule everywhere, say so early, because it changes the Cassandra configuration and the cost of running it.

## Cassandra and Hadoop integration: how the two connect

Searching for "Cassandra Hadoop integration" suggests one product. In practice it is a pipeline. Live data is written
to Cassandra and served from it. A batch or streaming job, usually Apache Spark with the Spark Cassandra Connector,
reads from Cassandra or from the event stream and writes history to HDFS or object storage as Parquet. Analysts and
models work on that history without touching the serving database. Keep the boundary explicit: Cassandra holds what the
application needs now, and the data lake holds everything else.

## HDFS or object storage in the cloud

On AWS, Azure or Google Cloud, the "HDFS" half of this comparison is often object storage (S3, ADLS, GCS) queried by
Spark, Trino or a warehouse, with no Hadoop cluster to run. The batch versus real-time trade-offs still apply. What
changes is who operates the storage layer, and that usually decides the running cost more than the software does.

## The team you have decides the running cost

A Cassandra cluster wants someone comfortable with repair schedules, compaction and capacity planning. A Hadoop or
Spark platform wants someone who can tune jobs and manage file layout. If you have neither skill in-house, the honest
comparison includes who will operate the system in year two.

---

Related on innerluxes.dev: [Cassandra vs Hadoop (HDFS)](https://innerluxes.dev/data/cassandra-vs-hadoop),
[Big data consulting](https://innerluxes.dev/data/big-data/consulting/),
[Cassandra performance](https://innerluxes.dev/data/cassandra-performance/).
