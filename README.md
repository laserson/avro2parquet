avro2parquet
============

Hadoop MapReduce program to convert [Avro][2] data files to [Parquet format][2].

Installation
------------

    git clone https://github.com/laserson/avro2parquet.git
    cd avro2parquet
    mvn clean package

This will generate the `jar` files in the `target/` directory.

Usage
-----

This tool will work on Avro container files (which I believe is just the
standard Avro data file format).  It contains the Avro `GenericRecord` objects
as the key and a `NullWritable` as the value.

The tool is currently hardcoded to output [Snappy-compressed][3] Parquet.  It is
simply a MapReduce job using the `Tool` interface.

The command is like so:

    hadoop jar <avro2parquet jar file> \
    com.cloudera.science.avro2parquet.Avro2Parquet \
    <and generic options to the JVM> \
    hdfs:///path/to/avro/schema.avsc \
    hdfs:///path/to/avro/data \
    hdfs:///output/path

so for example:

    hadoop jar avro2parquet-0.1.0-jar-with-dependencies.jar \
    com.cloudera.science.avro2parquet.Avro2Parquet \
    -D mapred.child.java.opts=-Xmx1024M \
    hdfs:///user/lasersou/schemas/data.avsc \
    hdfs:///user/lasersou/data \
    hdfs:///user/lasersou/output

[1]: http://avro.apache.org/
[2]: http://parquet.io/
[3]: https://code.google.com/p/snappy/