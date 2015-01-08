# dplyrimpaladb

dplyrimpaladb is a Database connector for ImpalaDB for dplyr the next iteration of plyr (from Hadley Wickham), focussed on tools for working with data frames (hence the `d` in the name).

## Installing dependencies

To be able to write tables to ImpalaDB you will need HDFS support provided by rhdfs - follow th installation instructions from https://github.com/RevolutionAnalytics/RHadoop/wiki.

The interface to ImpalaDB is driven by Hive JDBC.  This will require the driver to be installed, and one of the easiest ways to achieve this is by following the installation instructions provided by Cloudera here: http://cloudera.com/content/cloudera-content/cloudera-docs/Impala/latest/Installing-and-Using-Impala/ciiu_noncm_installation.html

You should only need to install the impala and impala-shell packages, unless you actually want to install a separate server.

## Install dependent R packages

Install RJDBC, devtools, and dplyr with:

* the latest released version from CRAN with

    ```R
    install.packages(c("RJDBC", "devtools", "dplyr"))
    ```

Now install dplyrimpaladb from github using devtools:

```R
devtools::install_github("jwills/dplyrimpaladb")
```

If you encounter a clear bug, please file a minimal reproducible example on [github](https://github.com/jwills/dplyrimpaladb/issues).

## Getting Started

Connect to the Database:

```R
library(dplyrimpaladb)

# Set the classpath for a local install:
options(dplyr.jdbc.classpath = "/usr/lib/impala")
# Alternatively, set the classpath for the ImpalaDB JDBC connector on a CDH cluster node:
options(dplyr.jdbc.classpath = "/opt/cloudera/parcels/CDH/lib/hive/lib/:/opt/cloudera/parcels/CDH/lib/hadoop/lib")

# To connect to a database first create a src:
gdelt <- src_impaladb(dbname='gdelt', host='localhost')
gdelt

# Simple Impala table retrieval
events <- tbl(gdelt, 'events')
events
```

See dplyr for many more examples.
