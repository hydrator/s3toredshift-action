# S3ToRedshift Action


Description
-----------
S3ToRedshift Action that will load the data from AWS S3 bucket into the AWS Redshift table.

Properties
----------

**accessKey:** Access key for AWS S3 to connect to. Either provide 'Keys(Access and Secret Access keys)' or 'IAM
Role' for connecting to AWS S3 bucket. (Macro-enabled)

**secretAccessKey:** Secret access key for AWS S3 to connect to. Either provide 'Keys(Access and Secret Access keys)'
 or 'IAM Role' for connecting to AWS S3 bucket. (Macro-enabled)

**iamRole:** IAM Role for AWS S3 to connect to. This can only be used if the cluster is hosted on AWS servers. Either
 provide 'Keys(Access and Secret Access keys)' or 'IAM Role' for connecting to AWS S3 bucket. (Macro-enabled)

**s3Region:** The region for AWS S3 to connect to. If not specified, then plugin will consider that S3 bucket is in
the same region as of the Redshift cluster. (Macro-enabled)

**s3DataPath:** The S3 path of the bucket where the data is stored and will be loaded into the Redshift table.
For example, 's3://bucket-name/test/' or 's3://bucket-name/test/2017-02-22/'(will load files present in specific
directory) or 's3://bucket-name/test'(will load the files having prefix ``test``) or
's3://bucket-name/test/2017-02-22'(will load files from ``test`` directory having prefix ``2017-02-22``).
(Macro-enabled)

**clusterDbUrl:** The JDBC Redshift database URL for Redshift cluster, where the table is present. For example,
'jdbc:redshift://x.y.us-west-2.redshift.amazonaws.com:5439/dev'. (Macro-enabled)

**masterUser:** Master user for the Redshift cluster to connect to. (Macro-enabled)

**masterPassword:** Master password for Redshift cluster to connect to. (Macro-enabled)

**tableName:** The Redshift table name where the data from the S3 bucket will be loaded. (Macro-enabled)

**listOfColumns:** Comma-separated list of the Redshift table column names to load the specific columns from S3
bucket. If not provided, then all the columns from S3 will be loaded into the Redshift table. (Macro-enabled)

Conditions
----------
Any invalid configurations for connecting to AWS S3 bucket or Redshift cluster, will result into the runtime failure.

Both configurations 'Keys(Access and Secret Access keys)' and 'IAM Role' can not be provided or empty at the same
time. Either provide 'Keys(Access and Secret Access keys)' or 'IAM Role' for connecting to AWS S3 bucket.

S3 data path should starts with s3://, not with s3n:// or s3a:// uri scheme.

Table must exists in the Redshift cluster, for loading the data. If not, then it will result into the runtime failure.

Schema of the table must match with S3 bucket data schema. If not, then it will result into the runtime failure.

Plugin supports only avro formatted data present in the S3 bucket to be loaded into the Redshift table and uses
'auto' option for formatting.

Example
-------
This example connects to a S3 instance using the 'accessKey and secretAccessKey', and to Redshift instance using
'clusterDbUrl, masterUser and masterPassword'. Data from the S3 bucket provided through 's3DataPath' will be loaded
into the Redshift table 'redshifttest'.

    {
      "name": "S3ToRedshift",
      "type": "action",
        "properties": {
          "accessKey": "access-key",
          "secretAccessKey": "secret-access-key",
          "s3DataPath": "s3://bucket-name/test/",
          "clusterDbUrl": "jdbc:redshift://x.y.us-west-2.redshift.amazonaws.com:5439/dev",
          "masterUser": "master-user",
          "masterPassword": "master-password",
          "tableName": "redshifttest"
        }
    }
