---
layout: post
title: 'Cassandra create table analysis'
date: '2019-07-14'
categories: cassandra
---

### Notes for create table statements

Query used

> CREATE TABLE %s (p text, c text, v text, s text static, PRIMARY KEY (p, c))

- System table definitions can be found in the `SchemaKeyspaces` class.
These tables are used internally for any schema change

https://github.com/apache/cassandra/blob/149caf01e08f58f306ff51379ab189c7a4b1ca6d/src/java/org/apache/cassandra/schema/SchemaKeyspace.java#L108

- Every change to schema calls the following method:
`Schema.transform(SchemaTransformation transformation, boolean locally, long now)`

This method essentially does the following:
1. Get the current `Keyspaces`
2. Apply a transformation and get the expected `Keyspaces`
3. Get `KeyspacesDiff` between current and expected `Keyspaces`
4. Convert the `KeyspacesDiff` to a generic `Collection<Mutation>`
5. Apply each `Mutation`
    - apply `PartitionUpdate` to commit log 
    `getWriteHandler().beginWrite(mutation, makeDurable)`
    - apply `PartitionUpdate` to memtable
    `cfs.getWriteHandler().write(upd, ctx, indexTransaction)`
6. Update version and announce
7. Broadcast change to other nodes

#### Mutation applied

```
[Mutation(keyspace='system_schema', key='63716c5f746573745f6b65797370616365', modifications=[
  [system_schema.columns] key=cql_test_keyspace partition_deletion=deletedAt=-9223372036854775808, localDeletion=2147483647 columns=[[] | [clustering_order column_name_bytes kind position type]]
    Row[info=[ts=1563086421518000] ]: table_name=table_0, column_name=c | [clustering_order=asc ts=1563086421518000], [column_name_bytes=63 ts=1563086421518000], [kind=clustering ts=1563086421518000], [position=0 ts=1563086421518000], [type=text ts=1563086421518000]
    Row[info=[ts=1563086421518000] ]: table_name=table_0, column_name=p | [clustering_order=none ts=1563086421518000], [column_name_bytes=70 ts=1563086421518000], [kind=partition_key ts=1563086421518000], [position=0 ts=1563086421518000], [type=text ts=1563086421518000]
    Row[info=[ts=1563086421518000] ]: table_name=table_0, column_name=s | [clustering_order=none ts=1563086421518000], [column_name_bytes=73 ts=1563086421518000], [kind=static ts=1563086421518000], [position=-1 ts=1563086421518000], [type=text ts=1563086421518000]
    Row[info=[ts=1563086421518000] ]: table_name=table_0, column_name=v | [clustering_order=none ts=1563086421518000], [column_name_bytes=76 ts=1563086421518000], [kind=regular ts=1563086421518000], [position=-1 ts=1563086421518000], [type=text ts=1563086421518000]

  [system_schema.keyspaces] key=cql_test_keyspace partition_deletion=deletedAt=-9223372036854775808, localDeletion=2147483647 columns=[[] | [durable_writes replication]]
    Row[info=[ts=1563086421518000] ]: EMPTY | [durable_writes=true ts=1563086421518000], [replication=0000000200000005636c6173730000002b6f72672e6170616368652e63617373616e6472612e6c6f6361746f722e53696d706c655374726174656779000000127265706c69636174696f6e5f666163746f720000000131 ts=1563086421518000]

  [system_schema.tables] key=cql_test_keyspace partition_deletion=deletedAt=-9223372036854775808, localDeletion=2147483647 columns=[[] | [additional_write_policy bloom_filter_fp_chance caching comment compaction compression crc_check_chance dclocal_read_repair_chance default_time_to_live extensions flags gc_grace_seconds id max_index_interval memtable_flush_period_in_ms min_index_interval read_repair read_repair_chance speculative_retry]]
    Row[info=[ts=1563086421518000] ]: table_name=table_0 | [additional_write_policy=99p ts=1563086421518000], [bloom_filter_fp_chance=0.01 ts=1563086421518000], [caching=00000002000000046b65797300000003414c4c00000012726f77735f7065725f706172746974696f6e000000044e4f4e45 ts=1563086421518000], [comment= ts=1563086421518000], [compaction=0000000300000005636c6173730000003f6f72672e6170616368652e63617373616e6472612e64622e636f6d70616374696f6e2e53697a65546965726564436f6d70616374696f6e53747261746567790000000d6d61785f7468726573686f6c640000000233320000000d6d696e5f7468726573686f6c640000000134 ts=1563086421518000], [compression=00000002000000126368756e6b5f6c656e6774685f696e5f6b6200000002313600000005636c6173730000002e6f72672e6170616368652e63617373616e6472612e696f2e636f6d70726573732e4c5a34436f6d70726573736f72 ts=1563086421518000], [crc_check_chance=1.0 ts=1563086421518000], [dclocal_read_repair_chance=0.0 ts=1563086421518000], [default_time_to_live=0 ts=1563086421518000], [extensions=00000000 ts=1563086421518000], [flags=0000000100000008636f6d706f756e64 ts=1563086421518000], [gc_grace_seconds=864000 ts=1563086421518000], [id=409569f0-a602-11e9-a19b-33a69b4152ed ts=1563086421518000], [max_index_interval=2048 ts=1563086421518000], [memtable_flush_period_in_ms=0 ts=1563086421518000], [min_index_interval=128 ts=1563086421518000], [read_repair=BLOCKING ts=1563086421518000], [read_repair_chance=0.0 ts=1563086421518000], [speculative_retry=99p ts=1563086421518000]
])]
```
 
  