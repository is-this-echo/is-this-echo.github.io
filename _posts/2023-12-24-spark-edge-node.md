https://stackoverflow.com/questions/42730820/spark-submit-on-edge-node

discuss about writing output dataframe csv from spark directly to edge node but it fails, so first have to write to hdfs then copy from here to edge node

issue because deploy mode = cluster, so it will save to any of the worker nodes, edge node may or may not be part of those nodes or the yarn cluster

https://www.phdata.io/blog/incremental-merge-with-apache-spark/

provide code that you have given, renaming files and moving, all those stuff