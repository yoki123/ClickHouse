---
toc_priority: 46
toc_title: UUID
---

# UUID {#uuid-data-type}

A universally unique identifier (UUID) is a 16-byte number used to identify records. For detailed information about the UUID, see [Wikipedia](https://en.wikipedia.org/wiki/Universally_unique_identifier).

The example of UUID type value is represented below:

``` text
61f0c404-5cb3-11e7-907b-a6006ad3dba0
```

If you do not specify the UUID column value when inserting a new record, the UUID value is filled with zero:

``` text
00000000-0000-0000-0000-000000000000
```

## How To Generate {#how-to-generate}

To generate the UUID value, ClickHouse provides the [generateUUIDv4](../../sql_reference/functions/uuid_functions.md) function.

## Usage Example {#usage-example}

**Example 1**

This example demonstrates creating a table with the UUID type column and inserting a value into the table.

``` sql
CREATE TABLE t_uuid (x UUID, y String) ENGINE=TinyLog
```

``` sql
INSERT INTO t_uuid SELECT generateUUIDv4(), 'Example 1'
```

``` sql
SELECT * FROM t_uuid
```

``` text
┌────────────────────────────────────x─┬─y─────────┐
│ 417ddc5d-e556-4d27-95dd-a34d84e46a50 │ Example 1 │
└──────────────────────────────────────┴───────────┘
```

**Example 2**

In this example, the UUID column value is not specified when inserting a new record.

``` sql
INSERT INTO t_uuid (y) VALUES ('Example 2')
```

``` sql
SELECT * FROM t_uuid
```

``` text
┌────────────────────────────────────x─┬─y─────────┐
│ 417ddc5d-e556-4d27-95dd-a34d84e46a50 │ Example 1 │
│ 00000000-0000-0000-0000-000000000000 │ Example 2 │
└──────────────────────────────────────┴───────────┘
```

## Restrictions {#restrictions}

The UUID data type only supports functions which [String](string.md) data type also supports (for example, [min](../../sql_reference/aggregate_functions/reference.md#agg_function-min), [max](../../sql_reference/aggregate_functions/reference.md#agg_function-max), and [count](../../sql_reference/aggregate_functions/reference.md#agg_function-count)).

The UUID data type is not supported by arithmetic operations (for example, [abs](../../sql_reference/functions/arithmetic_functions.md#arithm_func-abs)) or aggregate functions, such as [sum](../../sql_reference/aggregate_functions/reference.md#agg_function-sum) and [avg](../../sql_reference/aggregate_functions/reference.md#agg_function-avg).

[Original article](https://clickhouse.tech/docs/en/data_types/uuid/) <!--hide-->
