---
editable: false
sourcePath: en/_api-ref-grpc/mdb/clickhouse/v1/api-ref/grpc/Cluster/streamLogs.md
---

# Managed Service for ClickHouse API, gRPC: ClusterService.StreamLogs {#StreamLogs}

Same as ListLogs but using server-side streaming. Also allows for `tail -f` semantics.

## gRPC request

**rpc StreamLogs ([StreamClusterLogsRequest](#yandex.cloud.mdb.clickhouse.v1.StreamClusterLogsRequest)) returns (stream [StreamLogRecord](#yandex.cloud.mdb.clickhouse.v1.StreamLogRecord))**

## StreamClusterLogsRequest {#yandex.cloud.mdb.clickhouse.v1.StreamClusterLogsRequest}

```json
{
  "clusterId": "string",
  "columnFilter": [
    "string"
  ],
  "serviceType": "ServiceType",
  "fromTime": "google.protobuf.Timestamp",
  "toTime": "google.protobuf.Timestamp",
  "recordToken": "string",
  "filter": "string"
}
```

#|
||Field | Description ||
|| clusterId | **string**

Required field. Required. ID of the ClickHouse cluster. ||
|| columnFilter[] | **string**

Columns from logs table to get in the response. ||
|| serviceType | enum **ServiceType**

Required field. 

- `SERVICE_TYPE_UNSPECIFIED`
- `CLICKHOUSE`: Logs of ClickHouse activity. ||
|| fromTime | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

Start timestamp for the logs request. ||
|| toTime | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

End timestamp for the logs request.
If this field is not set, all existing logs will be sent and then the new ones as
they appear. In essence it has `tail -f` semantics. ||
|| recordToken | **string**

Record token. Set `recordToken` to the [StreamLogRecord.nextRecordToken](#yandex.cloud.mdb.clickhouse.v1.StreamLogRecord) returned by a previous StreamLogs
request to start streaming from next log record. ||
|| filter | **string**

A filter expression that filters resources listed in the response.
The expression must specify:
1. The field name. Currently filtering can be applied to the [LogRecord.logs.message.hostname], [LogRecord.logs.message.severity] fields.
2. An `=` operator.
3. The value in double quotes (`"`). Must be 1-63 characters long and match the regular expression `[a-z0-9.-]{1,61}`.
Examples of a filter:
- `message.hostname='node1.db.cloud.yandex.net'`
- `message.severity IN ('Error', 'Fatal') AND message.hostname != 'node2.db.cloud.yandex.net'`. ||
|#

## StreamLogRecord {#yandex.cloud.mdb.clickhouse.v1.StreamLogRecord}

```json
{
  "record": {
    "timestamp": "google.protobuf.Timestamp",
    "message": "string"
  },
  "nextRecordToken": "string"
}
```

#|
||Field | Description ||
|| record | **[LogRecord](#yandex.cloud.mdb.clickhouse.v1.LogRecord)**

One of the requested log records. ||
|| nextRecordToken | **string**

This token allows you to continue streaming logs starting from the exact
same record. To continue streaming, specify value of [next_record_token[
as value for the [StreamClusterLogsRequest.recordToken](#yandex.cloud.mdb.clickhouse.v1.StreamClusterLogsRequest) parameter in the next StreamLogs request.
This value is interchangeable with the [ListClusterLogsResponse.nextPageToken](/docs/managed-clickhouse/api-ref/grpc/Cluster/listLogs#yandex.cloud.mdb.clickhouse.v1.ListClusterLogsResponse) from ListLogs method. ||
|#

## LogRecord {#yandex.cloud.mdb.clickhouse.v1.LogRecord}

#|
||Field | Description ||
|| timestamp | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

Log record timestamp in [RFC3339](https://www.ietf.org/rfc/rfc3339.txt) text format. ||
|| message | **string**

Contents of the log record. ||
|#