---
id: create-source-s3
title: Ingest data from S3 buckets
description: Ingest data from S3 buckets
slug: /create-source-s3
---
Use the SQL statement below to connect RisingWave to an Amazon S3 source.

## Syntax

```sql
CREATE SOURCE [ IF NOT EXISTS ] source_name 
schema_definition
WITH (
   connector='s3',
   connector_parameter='value', ...
)
ROW FORMAT csv [WITHOUT HEADER] DELIMITED BY ','; 
```

**schema_definition**:
```sql
(
   column_name data_type [ PRIMARY KEY ], ...
   [ PRIMARY KEY ( column_name, ... ) ]
)
```

## Parameters

|Field|Notes|
|---|---|
|s3.region_name	|Required. The service region.|
|s3.bucket_name	|Required. The name of the bucket the data source is stored in.	|
|s3.credentials.access| Conditional. This field indicates the access key ID of AWS. It must be used with `s3.credentials.secret`. If not specified, RisingWave will automatically try to use `~/.aws/credentials`.|
|s3.credentials.secret| Conditional. This field indicates the secret access key of AWS. It must be used wtih `s3.credentials.access`. If not specified, RisingWave will automatically try to use `~/.aws/credentials`.|


## Example
Here is an example of connecting RisingWave to an S3 source to read data from individual streams.

```sql
CREATE TABLE s(
    id int,
    name varchar,
    age int,
    primary key(id)
) WITH (
    connector = 's3',
    s3.region_name = 'ap-southeast-2',
    s3.bucket_name = 'example-s3-source',
    s3.credentials.access = 'xxxxx',
    s3.credentials.secret = 'xxxxx'
) ROW FORMAT csv [WITHOUT HEADER] DELIMITED BY ',';
```