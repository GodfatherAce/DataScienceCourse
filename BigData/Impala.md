Impala
====================
Cloudera Impala is Cloudera's open source massively parallel processing (MPP) SQL query engine for data stored in a computer cluster running Apache Hadoop.[1]

Cloudera Impala is a query engine that runs on Apache Hadoop. The project was announced in October 2012 with a public beta test distribution[2][3] and became generally available in May 2013.[4]

The Apache-licensed Impala project brings scalable parallel database technology to Hadoop, enabling users to issue low-latency SQL queries to data stored in HDFS and Apache HBase without requiring data movement or transformation. Impala is integrated with Hadoop to use the same file and data formats, metadata, security and resource management frameworks used by MapReduce, Apache Hive, Apache Pig and other Hadoop software.

Impala is promoted for analysts and data scientists to perform analytics on data stored in Hadoop via SQL or business intelligence tools. The result is that large-scale data processing (via MapReduce) and interactive queries can be done on the same system using the same data and metadata – removing the need to migrate data sets into specialized systems and/or proprietary formats simply to perform analysis.

Features include:

- Supports HDFS and Apache HBase storage
- Reads Hadoop file formats, including text, LZO, SequenceFile, Avro, RCFile, and Parquet
- Supports Hadoop security (Kerberos authentication)
- Fine-grained, role-based authorization with Sentry[5]
- Uses metadata, ODBC driver, and SQL syntax from Apache Hive

In early 2013, a column-oriented file format called Parquet was announced for architectures including Impala.
In December 2013, Amazon Web Services announced support for Impala.
In early 2014, MapR added support for Impala.
