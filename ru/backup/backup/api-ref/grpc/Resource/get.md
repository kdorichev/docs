---
editable: false
sourcePath: en/_api-ref-grpc/backup/v1/backup/api-ref/grpc/Resource/get.md
---

# Cloud Backup API, gRPC: ResourceService.Get {#Get}

Get specific Compute Cloud instance.

## gRPC request

**rpc Get ([GetResourceRequest](#yandex.cloud.backup.v1.GetResourceRequest)) returns ([GetResourceResponse](#yandex.cloud.backup.v1.GetResourceResponse))**

## GetResourceRequest {#yandex.cloud.backup.v1.GetResourceRequest}

```json
{
  "computeInstanceId": "string"
}
```

#|
||Field | Description ||
|| computeInstanceId | **string**

Required field. Compute Cloud instance ID. ||
|#

## GetResourceResponse {#yandex.cloud.backup.v1.GetResourceResponse}

```json
{
  "resource": {
    "computeInstanceId": "string",
    "createdAt": "google.protobuf.Timestamp",
    "updatedAt": "google.protobuf.Timestamp",
    "online": "bool",
    "enabled": "bool",
    "status": "Status",
    "statusDetails": "string",
    "statusProgress": "int64",
    "lastBackupTime": "google.protobuf.Timestamp",
    "nextBackupTime": "google.protobuf.Timestamp",
    "resourceId": "string",
    "isActive": "bool",
    "initStatus": "InitStatus",
    "metadata": "string",
    "type": "ResourceType"
  }
}
```

#|
||Field | Description ||
|| resource | **[Resource](#yandex.cloud.backup.v1.Resource)**

Set of resource parameters. ||
|#

## Resource {#yandex.cloud.backup.v1.Resource}

#|
||Field | Description ||
|| computeInstanceId | **string**

Compute Cloud instance ID. ||
|| createdAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)** ||
|| updatedAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)** ||
|| online | **bool**

If this field is true, it means that instance is online. ||
|| enabled | **bool**

If this field is true, it means that backup is enabled to instance. ||
|| status | enum **Status**

- `STATUS_UNSPECIFIED`
- `IDLE`: Compute Cloud instance is doing nothing right now.
- `BACKUPING`: Compute Cloud instance is currently backing up itself.
- `RECOVERING`: Compute Cloud instance is currently recovering itself.
- `FAILED`: Compute Cloud instance is in failure state, check content of
`status_details` field for more information.
- `OTHER`: Unspecified state, check `status_details` field
for more information. ||
|| statusDetails | **string**

If status value is one of `OTHER` or `FAILED`,
detailed info might be stored here. ||
|| statusProgress | **int64**

In case status is one of `BACKUPING` or `RECOVERING`,
progress value might be found here. ||
|| lastBackupTime | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)** ||
|| nextBackupTime | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)** ||
|| resourceId | **string**

Resource ID is used to identify Compute Cloud instance in backup service. ||
|| isActive | **bool**

Status `is_active` shows whether current Compute Cloud instance controls Cloud Backup resource.
If status `is_active` is false it means Compute Cloud instance is not able to manipulate
Cloud Backup resource. ||
|| initStatus | enum **InitStatus**

Status of resource initialization in cloud backup service.

- `INIT_STATUS_UNSPECIFIED`
- `REGISTERING`: Registration of instance in cloud backups have started.
- `REGISTRED`: Instance is registered in cloud backups.
- `FAILED_REGISTRATION`: Instance registration failed.
- `DELETED`: Instance is deleted from cloud backup service. ||
|| metadata | **string**

Metadata to provide details about instance registration process
if status is FAILED_REGISTRATION or REGISTERING ||
|| type | enum **ResourceType**

Type of resource. Could be compute VM or baremetal server.

- `RESOURCE_TYPE_UNSPECIFIED`
- `COMPUTE`: Resource is Compute Cloud VM
- `BMS`: Resource is baremetal server ||
|#